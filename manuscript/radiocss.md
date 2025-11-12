# RadioCss

Es un enum con los estilos para label y radio que se usaran

```java
public enum RadioCss {
    Label("ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"),
    Input("w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"),
    Div("flex items-center mb-4");
    
    public final String css;

    private RadioCss(String css) {
        this.css = css;
    }
}




```

Se usa con el elemento [RadioItem](radioitem.md)
