# Stepper

El componente Stepper, muestra un paso a paso.Se usa cuando son actividades que requieren realizar una tarea en orden.

Se basa en [Tailwind CSS Stepper - Flowbite](https://flowbite.com/docs/components/stepper/)

Por ejemplo

![](resources/stepper/00.png)

Se cuenta con un record, que recibe los valores a mostrar.

```java
public record StepperData(String leftValue, String title, String subTitle, Boolean active  ) {

}


```

Para implementarlo en jettraui debemos pasar un List<StepperData>





```java
  List<StepperData> stepperDatas = new ArrayList<>();
           
 stepperDatas.add(new StepperData("1", "Motivo del Estudio", "Seleccione uno", Boolean.TRUE));
 stepperDatas.add(new StepperData("2", "Data", "Esto es", Boolean.FALSE));
 
 mainForm.add(new Stepper(stepperDatas));


```

Genera

![](resources/stepper/01.png)



Si deseas construirlo sin el componente Stepper lo puedes usar mediante

```java
  O o = new O("items-center w-full space-y-4 sm:flex sm:space-x-8 sm:space-y-0 rtl:space-x-reverse")
                    .add(
                            new Li("flex items-center text-blue-600 dark:text-blue-500 space-x-2.5 rtl:space-x-reverse")
                                    .add(new Span("flex items-center justify-center w-8 h-8 border border-blue-600 rounded-full shrink-0 dark:border-blue-500").text("1"))
                                    .add(new Span()
                                            .add(new H3().text("Motivo del estudio").style("font-medium leading-tight"))
                                            .add(new P().addClass("text-sm").text("Seleccione uno"))
                                    )
                    );
            mainForm.add(o);


```