# Prompt


necesito que crees un nuevo framework java pero solo con flowbite elimina bootstrap, deseo que tenga un navbar con opciones responsibas menu hamburguesa ,que muestra una opcion de notificaciones con un contador numerico, el siguiente elemento debe ser la opcion de cambiar tema de dark a ligth luego el nombre del usuario logeado y un boton logout.

En cuanto al sidebar deben tener secciones dividas donde se encuentren los elementos con iconos y texto para invocar las paginas estos elementos deben ser responsivos, y debe tener un footer que pueda personalizar pasando atrabitutos como texto e iconos.

Tambien debes soportar iconos para pasarle. 

Ademas debe tener la parte de contenido que se mostrara en cada pagina que se invoque y contenga la implementacion del dashboard creado. 

Todo debe ser generado desde clases en java que generen componentes como DIV, BUTTON, INPUTTEXT, SIDEBAR, FOOTER, NAVBAR, y el contenido que debe ser responsivo, recuerda que el framework se implementara sobre jakarta ee y eclipse microprofile, ademas crea la pagina de login recuerda que todo debe ser codigo java , la pagina de acceso denegado.

crea una pagina con un  formulario de ejemplo con label inputtext fileupload, botones, dialogos de confirmacion otro formulario que contenga un datatable ,recuerda que todos los compontes son codigo java no usaras ninguna pagina html. Debe ser un diseño simplificado el proyecto debe usar maven

# Trabajo


Por favor analiza este proyecto  es un framnework para generar interfaces web en java utiliza Flowbite CSS, los diversos componentes generan la interface del cliente permitiendo desde Java crear los componentes, se integra con Jakarta EE y Eclipse Microprofile.. Estudialo y analizalo para ser usado te dare un ejemplo de su implementacion, ya que creo la libreria y esta la integro en otro proyecto,
@Path("jettra-view") // ⭐ Define la URL final: /api/profile-view
@RequestScoped
public class JettraViewExampleView extends JettraView {
    // <editor-fold defaultstate="collapsed" desc="attributes()">

    WebModelSession webModelSession = new WebModelSession();
    List<Tag> headers = new ArrayList<>();
    @Inject
    ConfigurationProperties configurationProperties;
// </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="String init()">

    @Override
    protected String init() {

        webModelSession = webModelOfSession(request);

        return DashboardLayout.buildPage(
                request,
                webModelSession.getUsername(),
                content(request),
                MenuSideBar.getSidebarSections(
                        this.getClass().getSimpleName(),
                        webModelSession
                ),
                "Jetrra View Example",
                configurationProperties.getDashboardFooterText() + " | " + webModelSession.getUserRol(),
                headers
        );

    }
// </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="protected WebComponent content(HttpServletRequest request)">
    @Override
    protected WebComponent content(HttpServletRequest request) {
        WebComponent mainContent = null;
        try {
            mainContent = new Tag("div").withText("Vista generada con JAX-RS y WebComponents para: " + webModelSession.getUsername());

            mainContent = new Panel("Fecth", mainContent, request);
        } catch (Exception e) {
            System.out.println("\t content() " + e.getLocalizedMessage());
        }
        return mainContent;
    }
// </editor-fold>

    @Override
    protected String javaScriptCode() {
        throw new UnsupportedOperationException("Not supported yet."); // Generated from nbfs://nbhost/SystemFileSystem/Templates/Classes/Code/GeneratedMethodBody
    }
}

analiza el proyecto