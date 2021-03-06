
# Header only C++17 benchmarking

## __C style function returning non void__

```cpp
double alternating_harmonic_series()
{
    double sum = 0.0;

    for (std::size_t i = 1UL; i < ITERATIONS + 1UL; i++)
    {
        if (i % 2UL)
            sum += 1.0 / static_cast<double>(i);
        else
            sum -= 1.0 / static_cast<double>(i);
    }

    return sum;
}

auto [ms, sum] = massiva::benchmark(alternating_harmonic_series);

std::printf("{ %9.4lf ms } The partial sum of the first %lu terms is %7.6lf\n", ms, ITERATIONS, sum);
```

    {  821.8700 ms } The partial sum of the first 100000000 terms is 0.693147

## __Callable object returning void__

```cpp
auto madhava_leibniz_series = [](double& sum) -> void
{
    sum = 0.0;

    for (std::size_t i = 0UL; i < ITERATIONS; i++)
    {
        if (i % 2UL)
            sum -= 4.0 / (2.0 * static_cast<double>(i) + 1.0);
        else
            sum += 4.0 / (2.0 * static_cast<double>(i) + 1.0);
    }
};

double sum;

auto ms = massiva::benchmark(madhava_leibniz_series, sum);

std::printf("{ %9.4lf ms } The partial sum of the first %lu terms is %7.6lf\n", ms, ITERATIONS, sum);

```

    { 1109.7230 ms } The partial sum of the first 100000000 terms is 3.141593

## License

The project is licensed under the [MIT License](https://opensource.org/licenses/MIT)
