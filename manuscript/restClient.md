#  RestClient


Para comunicarnos con el End-point sin autentificacion usamos.

Usaremos una clase llamada Motivo


```java

@Entity
public class Motivo {

    @Id(strategy = GenerationType.AUTO)
    private Long idmotivo;

    @Column
    private String motivo;

    @Column
    private Boolean activo;

    public Motivo() {
    }

    public Motivo(Long idmotivo, String motivo, Boolean activo) {
        this.idmotivo = idmotivo;
        this.motivo = motivo;
        this.activo = activo;
    }

//set/get

}


```

## Endpoint

El enpoint al que desea conectarse lo reivsamos mediante http://localhost:8080/openapi-ui/index.html

y es 

```shell

curl -X 'GET' \
  'http://localhost:8080/motivo' \
  -H 'accept: application/json'

```

p mediante http

```shell
http://localhost:8080/motivo
```

Utilice el ip de su computadora.

## microprofile-config.properties

Añada al archivo microprofile-config.properties

```
# RestClient
#

fish.payara.restclient.MotivoRestClient/mp-rest/url=http://127.0.0.1:8080/

```


## RestClient

Ahora cree en el paquete fish.payara.restclient la clase MotivoRestClient

```java
package fish.payara.restclient;

import fish.payara.model.Motivo;
import jakarta.ws.rs.DELETE;
import jakarta.ws.rs.GET;
import jakarta.ws.rs.POST;
import jakarta.ws.rs.PUT;
import jakarta.ws.rs.Path;
import jakarta.ws.rs.PathParam;
import jakarta.ws.rs.Produces;
import jakarta.ws.rs.QueryParam;
import jakarta.ws.rs.core.MediaType;
import jakarta.ws.rs.core.Response;
import java.util.List;
import org.eclipse.microprofile.openapi.annotations.enums.SchemaType;
import org.eclipse.microprofile.openapi.annotations.media.Content;
import org.eclipse.microprofile.openapi.annotations.media.Schema;
import org.eclipse.microprofile.openapi.annotations.parameters.Parameter;
import org.eclipse.microprofile.openapi.annotations.parameters.RequestBody;
import org.eclipse.microprofile.rest.client.inject.RegisterRestClient;

/**
 *
 * @author avbravo
 */
@RegisterRestClient()
@Path("/motivo")
//@ClientHeaderParam(name = "Authorization", value = "{lookupAuth}")
public interface MotivoRestClient {
   

    // <editor-fold defaultstate="collapsed" desc="findAll">
    @GET
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public List<Motivo> findAll();
// </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="Motivo findByIdmotivo">
    @GET
    @Path("{idmotivo}")

    public Motivo findByIdmotivo(
            @Parameter(description = "El idmotivo", required = true, example = "1", schema = @Schema(type = SchemaType.NUMBER)) @PathParam("idmotivo") Long idmotivo);

// </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="Motivo findByMotivo">
    @GET
    @Path("motivo")
    public Motivo findByMotivo(@Parameter(description = "El motivo", required = true, example = "1", schema = @Schema(type = SchemaType.STRING)) @QueryParam("motivo") final String motivo);
//// </editor-fold>

// <editor-fold defaultstate="collapsed" desc="List<Motivo> lookup(@QueryParam("filter") String filter, @QueryParam("sort") String sort, @QueryParam("page") Integer page, @QueryParam("size") Integer size)">
    @GET
    @Path("lookup")
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})

    public List<Motivo> lookup(@QueryParam("filter") String filter, @QueryParam("sort") String sort, @QueryParam("page") Integer page, @QueryParam("size") Integer size);

    // </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="Response save">
    @POST
    public Response save(
            @RequestBody(description = "Crea un nuevo motivo.", content = @Content(mediaType = "application/json", schema = @Schema(implementation = Motivo.class))) Motivo motivo);
// </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="Response update">

    @PUT

    public Response update(
            @RequestBody(description = "Crea un nuevo motivo.", content = @Content(mediaType = "application/json", schema = @Schema(implementation = Motivo.class))) Motivo motivo);
// </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="Response delete">
    @DELETE

    @Path("{idmotivo}")

    public Response delete(
            @Parameter(description = "El elemento idmotivo", required = true, example = "1", schema = @Schema(type = SchemaType.NUMBER)) @PathParam("idmotivo") Long idmotivo);
    // </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="Long count(@QueryParam("filter") String filter, @QueryParam("sort") String sort, @QueryParam("page") Integer page, @QueryParam("size") Integer size)">
    @GET
    @Path("count")
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})

    public Long count(@QueryParam("filter") String filter, @QueryParam("sort") String sort, @QueryParam("page") Integer page, @QueryParam("size") Integer size);

    // </editor-fold>
// </editor-fold>
    // <editor-fold defaultstate="collapsed" desc=" List<MotivoView> likeByName(@QueryParam("name") String name)">
    @GET
    @Path("likebyname")

    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})

    public List<Motivo> likeByName(@QueryParam("motivo") String motivo);

    // </editor-fold>
}


```

## Services

```java
package fish.payara.services;

import fish.payara.model.Motivo;
import java.util.List;
import java.util.Optional;
import org.bson.Document;
import org.bson.conversions.Bson;

/**
 *
 * @author avbravo
 */
public interface MotivoServices {

    public List<Motivo> findAll();

    public Optional<Motivo> findByIdmotivo(Long idmotivo);

    public Optional<Motivo> findByMotivo(String motivo);

    public Optional<Motivo> save(Motivo motivo);

    public Boolean update(Motivo motivo);

    public Boolean delete(Long idmotivo);

    public List<Motivo> lookup(Bson filter, Document sort, Integer page, Integer size);

    public Long count(Bson filter, Document sort, Integer page, Integer size);


}

```
## ServicesImplementation

```java
package fish.payara.services.implementation;

//import com.avbravo.jmoordbutils.encode.EncodeUtil;
import com.jmoordb.core.ui.properties.JettraResourcesFiles;
import com.jmoordb.core.ui.util.JettraUIUtil;
import com.jmoordb.core.ui.util.encode.EncodeUtil;
//import com.sft.restclient.MotivoRestClient;
import fish.payara.model.Motivo;
import fish.payara.restclient.MotivoRestClient;
import fish.payara.services.MotivoServices;
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Inject;
import jakarta.ws.rs.core.Response;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import org.bson.Document;
import org.bson.conversions.Bson;

/**
 *
 * @author avbravo
 */
@ApplicationScoped
public class MotivoServicesImpl implements MotivoServices {
    // <editor-fold defaultstate="collapsed" desc="@Inject">
@Inject
    private JettraResourcesFiles jrf;
    // </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="Microprofile Rest Client">
    @Inject
    MotivoRestClient motivoRestClient;
// </editor-fold>

    @Override
    public List<Motivo> findAll() {
        return motivoRestClient.findAll();
    }

    @Override
    public Optional<Motivo> findByIdmotivo(Long idmotivo) {
        try {
            Motivo result = motivoRestClient.findByIdmotivo(idmotivo);
            if (result == null || result.getIdmotivo() == null) {

            } else {
                return Optional.of(result);
            }
        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return Optional.empty();
    }
    
    @Override
    public Optional<Motivo> findByMotivo(String motivo) {
        try {
            Motivo result = motivoRestClient.findByMotivo(motivo);
            if (result == null || result.getIdmotivo() == null) {

            } else {
                return Optional.of(result);
            }
        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return Optional.empty();
    }

  

    // <editor-fold defaultstate="collapsed" desc="Optional<Motivo> save(Motivo motivo)">
    @Override
    public Optional<Motivo> save(Motivo motivo) {

        try {

            Response response = motivoRestClient.save(motivo);

            if (response.getStatus() == 400) {

                String error = (response.readEntity(String.class));

                return Optional.empty();
            }

            Motivo result = (Motivo) (response.readEntity(Motivo.class));

            return Optional.of(result);

        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return Optional.empty();

    }
    // </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="Boolean update(Motivo motivo)">
    @Override
    public Boolean update(Motivo motivo) {
        Boolean result = Boolean.FALSE;
        try {

            Integer status = motivoRestClient.update(motivo).getStatus();

            if (status == 201) {
                result = Boolean.TRUE;
            }

        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return result;
    }

    // </editor-fold>
    // <editor-fold defaultstate="collapsed" desc="Boolean delete(Long idmotivo)">
    @Override
    public Boolean delete(Long idmotivo) {
        Boolean result = Boolean.FALSE;
        try {

            Integer status = motivoRestClient.delete(idmotivo).getStatus();

            if (status == 201) {
                result = Boolean.TRUE;
            }

        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return result;
    }
    // </editor-fold>

    // <editor-fold defaultstate="collapsed" desc="List<Motivo> lookup(Bson filter, Document sort, Integer page, Integer size)">
    @Override
    public List<Motivo> lookup(Bson filter, Document sort, Integer page, Integer size) {
        List<Motivo> motivoList = new ArrayList<>();
        try {
          
            motivoList = motivoRestClient.lookup(
                    EncodeUtil.encodeBson(filter),
                    EncodeUtil.encodeBson(sort),
                    page, size);
        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return motivoList;
    }
// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="Long count(Bson filter, Document sort, Integer page, Integer size)">

    @Override
    public Long count(Bson filter, Document sort, Integer page, Integer size) {
        Long result = 0L;
        try {
            result = motivoRestClient.count(
                    EncodeUtil.encodeBson(filter),
                    EncodeUtil.encodeBson(sort),
                    page, size);
        } catch (Exception e) {
            JettraUIUtil.errorMessage(JettraUIUtil.nameOfClassAndMethod() + " " + e.getLocalizedMessage());
        }
        return result;
    }

    // </editor-fold>
 

   
}


```


## Ejemplo de Uso

```java

    @Inject
    MotivoServices motivoServices;

      List<Motivo> motivos = motivoServices.findAll();
        if(motivos== null || motivos.isEmpty()){
            
        }else{
            for(Motivo m:motivos){
                System.out.println("\t "+m.getMotivo());
            }
        }


```

