#  Radio 

Nos basarems en el componente [Tailwind CSS Radio - Flowbite](https://flowbite.com/docs/forms/radio/)

# Usando Div

```java

   Div divReasonSection = new Div().id("reason-section")
                    .add(new FieldSet().text("Motivo del estudio"))
                    .add(
                            new Div().addClass("radio-group-container two-columns")
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo1").name("motivo").required(Boolean.TRUE).value("Vaginitis"))
                                                    .add(new Label().forField("motivo1").text("Vaginitis").addClass(GridColCss.Label.css))
                                    )
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo2").name("motivo").required(Boolean.TRUE).value("Candidiasis previa"))
                                                    .add(new Label().forField("motivo2").text("Candidiasis previa").addClass(GridColCss.Label.css))
                                    )
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo3").name("motivo").required(Boolean.TRUE).value("Coitorragia"))
                                                    .add(new Label().forField("motivo3").text("Coitorragia").addClass(GridColCss.Label.css))
                                    )
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo4").name("motivo").required(Boolean.TRUE).value("Dispareunia"))
                                                    .add(new Label().forField("motivo4").text("Dispareunia").addClass(GridColCss.Label.css))
                                    )
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo5").name("motivo").required(Boolean.TRUE).value("Disuaria/Cistitis"))
                                                    .add(new Label().forField("motivo5").text("Disuaria/Cistitis").addClass(GridColCss.Label.css))
                                    )
                                    .add(
                                            new Div().addClass("radio-item")
                                                    .add(new RadioItem().id("motivo6").name("motivo").required(Boolean.TRUE).value("Gestante"))
                                                    .add(new Label().forField("motivo6").text("Gestante").addClass(GridColCss.Label.css))
                                    )
                    );
            mainForm.add(divReasonSection);

``


* disable
*checked
* Radio link #
* Helper text #
* Bordered 
* Radio list group 
* Horizontal list group
* Radio in dropdown
* Inline layout
* Advanced layout
* Colors 
