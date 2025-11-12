# RadioItem

Son elementos de botones de radio, se usan dentro de un [Radio](radio.md) y se acompañan 
con [RadioCss](radiocss.md)

La clase RadioItem, se debe indicar el id, el name, la etiqueta css.

* Para opciones desabilitada use **.disabled(Boolean.TRUE)**
* Elemento seleccionado por defecto **.checked(Boolean.TRUE)**




```java
Form mainForm = new Form().id("mainForm");
H3 h3 = new H3("Frutas");
Radio radioManzana = new Radio()
        .add(new RadioItem("manzana", "frutas", RadioCss.Input.css).disabled(Boolean.TRUE))
        .add(new Label("Manzana", RadioCss.Label.css, "manzana"));

Radio radioUva = new Radio()
        .add(new RadioItem("uva", "frutas", RadioCss.Input.css).checked(Boolean.TRUE))
        .add(new Label("Uva", RadioCss.Label.css, "uva"));
Radio radioPera = new Radio()
        .add(new RadioItem("pera", "frutas", RadioCss.Input.css).checked(Boolean.TRUE))
        .add(new Label("Pera", RadioCss.Label.css, "pera"));

mainForm.add(h3);
mainForm.add(radioManzana);
mainForm.add(radioUva);
mainForm.add(radioPera);
```
![](resources/radio/01.png)