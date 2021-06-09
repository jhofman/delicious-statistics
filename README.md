We opened a bag of m\&m candies today and saw what looked like a
surprisingly large number of green m\&ms\!

![bag of m\&ms](bag_of_m_and_ms.jpg)

So we decided to count them. We made one “bar” for each color, where
each bar was 3 m\&ms wide. It was tough to resist eating them in the
process.

![histogram of m\&m colors](m_and_m_colors.jpg) ![counts of m\&m
colors](data.jpg)

Then we tallied up all of the numbers, entered them into our computer,
and made a fancy bar plot. The toughest (and most important) part was
getting the official m\&m color codes so things looked pretty.

``` r
plot_data <- tribble(
  ~color, ~count, ~hex_code,
  "Red", 19, "#b11224",
  "Orange", 66,"#f26f22",
  "Yellow", 34, "#fff200",
  "Green", 81, "#31ac55",
  "Blue", 15, "#2f9fd7",
  "Brown", 22, "#603a34"
)

plot_data <- plot_data %>%
  mutate(color = factor(color, levels = color))

ggplot(plot_data, aes(x = color, y = count, color = color, fill = color)) +
  geom_bar(stat = "identity", width = 0.5) +
  geom_text(aes(label = count), vjust = -1) +
  scale_color_manual(values = plot_data$hex_code) +
  scale_fill_manual(values = plot_data$hex_code) +
  scale_y_continuous(breaks = seq(0, 80, 5)) +
  labs(x = "M & M color",
       y = "Number of M & Ms in the package") +
  theme_minimal() +
  theme(legend.position = "none",
        axis.text.x = element_text(color = plot_data$hex_code))
```

    ## Warning: Vectorized input to `element_text()` is not officially supported.
    ## Results may be unexpected or may change in future versions of ggplot2.

![](README_files/figure-gfm/fancy-m-and-m-color-histogram-1.png)<!-- -->

``` r
ggsave(file = 'm_and_m_colors.pdf', width = 6.5, height = 5.5)
```

Our conclusion was that our initial hunch was right. There is a really
uneven distribution of m\&m colors with lots of greens and oranges but
few blues, browns, and reds. So it seems like the factory might not be
trying to distribute colors evenly. Now we’re wondering why that is. Is
it easier or cheaper to make green m\&ms than blue ones?\!
