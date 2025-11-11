# Iconos



## FontAwesomeIcon

En el enum public enum FontAwesomeIcon , se han agregado algunos iconos de FontAwesome.

[https://fontawesome.com/icons](https://fontawesome.com/icons)


Se puede obtener el icono mediante

```java
String iconClass = FontAwesomenIconUtil.toIcon(FontAwesomeIcon.FA_S_IMAGE);

 System.out.println("Icono de Imagen (Clase CSS): " + iconClass); 
// Otro ejemplo con un icono 'regular' 

String heartClass = FontAwesomenIconUtil.toIcon(FontAwesomeIcon.FA_R_HEART); 
System.out.println("Icono de Corazón (Clase CSS): " + heartClass); 

// Ejemplo opcional con la etiqueta HTML 

String htmlTag = FontAwesomenIconUtil.toHtmlTag(FontAwesomeIcon.FA_S_HOUSE); 

System.out.println("Icono de Casa (Etiqueta HTML): " + htmlTag); }

```


* Para usarlo con opciones de menu


```java
mainLinks.add(new MenuLink("Dashboard", "/api/dashboard", isActive(currentController,DashboardView.class), FontAwesomeIcon.FA_S_TACHOMETER_ALT));

```




## FlowbiteIconSvg

Nota: No esta implementando aun.