---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: standard keys, import keys, encryption keys, Hyper Protect Crypto Services GUI

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Importación de claves estándar
{: #import-standard-keys}

Se pueden añadir claves de cifrado existentes mediante la interfaz gráfica de usuario de {{site.data.keyword.hscrypto}} o mediante programación con la API de {{site.data.keyword.hscrypto}}.

## Importación de claves estándar con la interfaz gráfica de usuario
{: #gui}

[Después de crear una instancia del servicio](/docs/services/hs-crypto/provision.html), siga los siguientes pasos para especificar su clave estándar existente con la interfaz gráfica de usuario de {{site.data.keyword.hscrypto}}.

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/){: new_window}.
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.hscrypto}}.
3. Para importar una nueva clave, pulse **Añadir clave** y, a continuación, seleccione la ventana **Especificar clave existente**.

    Especifique los detalles de la clave:

    <table>
      <tr>
        <th>Valor</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>
          <p>Un alias descriptivo exclusivo para identificar con facilidad su clave.</p>
          <p>Para proteger su privacidad, asegúrese de que el nombre de clave no contiene información de identificación personal (PII), como el nombre o la ubicación.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Tipo de clave</a> que desea gestionar en {{site.data.keyword.hscrypto}}. En la lista de tipos de claves, seleccione <b>Clave estándar</b>.</td>
      </tr>
      <tr>
        <td>Material de la clave</td>
        <td>
          <p>El material de la clave codificado en base64 como, por ejemplo, una clave simétrica, que desea gestionar en el servicio.</p>
          <p>Asegúrese de que el material de la clave cumple los requisitos siguientes:</p>
          <p><ul>
              <li>El tamaño de la clave puede ser de hasta 10,000 bytes.</li>
              <li>Los bytes de los datos deben estar codificados en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe los valores de <b>Generar nueva clave</b></caption>
    </table>

4. Cuando haya terminado de cumplimentar los detalles de la clave, pulse **Generar clave** para confirmar.

## Creación de claves estándar con la API
{: #api}

Cree una clave estándar realizando una llamada `POST` al siguiente punto final:

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio](/docs/services/hs-crypto/access-api.html).

1. Llame a la [API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} con el mandato de cURL siguiente.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<alias_clave>",
       "description": "<descripción_clave>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<material_clave>",
       "extractable": <tipo_clave>
       }
     ]
    }'
    ```
    {: codeblock}

    Para trabajar con claves dentro de un espacio y organización de Cloud Foundry en su cuenta, sustituya `Bluemix-Instance` con las cabeceras adecuadas de `Bluemix-org` y `Bluemix-space`. [Para obtener más información, consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.
    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><varname>región</varname></td>
        <td>La abreviatura de región, como <code>us-south</code> o <code>eu-gb</code>, que representa el área geográfica donde reside su instancia de servicio de {{site.data.keyword.hscrypto}}. Para obtener más información, consulte <a href="/docs/services/hs-crypto/regions.html#endpoints">Puntos finales de servicio regionales</a>.</td>
      </tr>
      <tr>
        <td><varname>señal_IAM</varname></td>
        <td>Su señal de acceso de {{site.data.keyword.cloud_notm}}. Incluya el contenido completo de la señal <code>IAM</code>, incluido el valor de Bearer, en la solicitud cURL. Para obtener más información, consulte <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Recuperación de una señal de acceso</a>.</td>
      </tr>
      <tr>
        <td><varname>ID_instancia</varname></td>
        <td>El identificador exclusivo que está asignado a su instancia de servicio de {{site.data.keyword.hscrypto}}. Para obtener más información, consulte <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Recuperación de un ID de instancia</a>.</td>
      </tr>
      <tr>
        <td><varname>ID_correlación</varname></td>
        <td>El identificador exclusivo que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><varname>preferencia_retorno</varname></td>
        <td><p>Opcional: una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Cuando establece la variable <em>preferencia_retorno</em> en <code>return=minimal</code>, el servicio solo devuelve los metadatos de la clave como, por ejemplo, el nombre de clave y valor de ID, en el cuerpo de entidad de la respuesta. Cuando establece la variable en <code>return=representation</code>, el servicio devuelve tanto el material de la clave como los metadatos de la clave.</p></td>
      </tr>
      <tr>
        <td><varname>alias_clave</varname></td>
        <td>
          <p>Nombre descriptivo exclusivo para identificar con facilidad su clave.</p>
          <p>Importante: Para proteger su privacidad, no almacene datos personales como metadatos para la clave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>descripción_clave</varname></td>
        <td>
          <p>Opcional: Una descripción ampliada para su clave.</p>
          <p>Importante: Para proteger su privacidad, no almacene datos personales como metadatos para la clave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>DD-MM-AAA</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Opcional: Fecha y hora de caducidad de la clave en el sistema, en formato RFC 3339. Si el atributo <code>expirationDate</code> se omite, la clave no caducará. </td>
      </tr>
      <tr>
        <td><varname>material_clave</varname></td>
        <td>
          <p>El material de la clave codificado en base64 como, por ejemplo, una clave simétrica, que desea gestionar en el servicio.</p>
          <p>Asegúrese de que el material de la clave cumple los requisitos siguientes:</p>
          <p><ul>
              <li>El tamaño de la clave puede ser de hasta 10,000 bytes.</li>
              <li>Los bytes de los datos deben estar codificados en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>tipo_clave</varname></td>
        <td>
          <p>Valor booleano que determina si el material de clave puede dejar el servicio.</p>
          <p>Cuando establece el atributo <code>extractable</code> en <code>true</code>, el servicio designa la clave como una clave estándar que puede almacenar en sus apps o servicios.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 2. Describe las variables necesarias para añadir una clave estándar con la API de {{site.data.keyword.hscrypto}}</caption>
    </table>

    Para proteger la confidencialidad de sus datos personales, evite especificar información de identificación personal (PII), como el nombre o la ubicación, cuando añades claves al servicio. Para obtener más ejemplos sobre la PII, consulte la sección 2.2 de la [NIST Special Publication 800-122 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Una respuesta `POST /v2/keys` satisfactoria devuelve el valor del ID para la clave, junto con otros metadatos. El ID es un identificador exclusivo que se asigna a su clave y que posteriores llamadas lo utilizan para la API de {{site.data.keyword.hscrypto}}.

2. Opcional: Verifique que la clave se ha añadido ejecutando la siguiente llamada para obtener las claves en su instancia de servicio de {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### Qué hacer a continuación

- Para obtener más información sobre cómo gestionar las claves mediante programación, [consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
- Para ver un ejemplo de cómo se almacenan las claves en {{site.data.keyword.hscrypto}} para cifrar y descifrar datos [consulte la app de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
