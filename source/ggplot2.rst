5 ggplot2
===============


5.1 介绍
------------------

用于分隔 ggplot2 图层的 ``+`` 的代码风格建议与管道中 ``%>%`` 的代码风格建议非常相似。


5.2 空格
------------

``+`` 前面应该总是有一个空格，后面应该有一个新行。即使你的图像只有两个图层也是如此。在第一步之后，每行应该缩进两个空格。

如果您正在创建 dplyr 管道的 ggplot，那么应该只有一个缩进级别。

.. code-block:: R

    # Good
    iris %>%
        filter(Species == "setosa") %>%
        ggplot(aes(x = Sepal.Width, y = Sepal.Length)) +
        geom_point()

    # Bad
    iris %>%
        filter(Species == "setosa") %>%
        ggplot(aes(x = Sepal.Width, y = Sepal.Length)) +
            geom_point()

    # Bad
    iris %>%
        filter(Species == "setosa") %>%
        ggplot(aes(x = Sepal.Width, y = Sepal.Length)) + geom_point()


5.3 长的行
----------------

如果 ggplot2 图层的参数不能全部放在一行，请将每个参数放在自己的行上并缩进：

.. code-block:: R

    # Good
    ggplot(aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
        geom_point() +
        labs(
            x = "Sepal width, in cm",
            y = "Sepal length, in cm",
            title = "Sepal length vs. width of irises"
        ) 

    # Bad
    ggplot(aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
        geom_point() +
        labs(x = "Sepal width, in cm", y = "Sepal length, in cm", title = "Sepal length vs. width of irises") 

ggplot2 允许您在 ``data`` 参数内进行数据操作，例如过滤或切片。请不要使用这种方式，应该在开始绘制之前在管道中执行数据操作。

.. code-block:: R

    # Good
    iris %>%
        filter(Species == "setosa") %>%
        ggplot(aes(x = Sepal.Width, y = Sepal.Length)) +
        geom_point()

    # Bad
    ggplot(filter(iris, Species == "setosa"), aes(x = Sepal.Width, y = Sepal.Length)) +
        geom_point()
