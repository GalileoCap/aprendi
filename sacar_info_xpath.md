# Sacar información de paginas web usando XPath
## Descripcion
* Puedo buscar entre los elementos usando la función:  
`function getElementByXPath(path) {`  
` return document.evaluate(path, document, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);`  
`}`
* Por ejemplo, si quiero buscar todos los elementos que contengan la palabra "Hola", la llamo con el path= '//*[text()[contains(.,"Hola")]]' y la guardo en una variable  
`var Hola= '//*[text()[contains(.,"Hola")]]';`  
`var tienen_hola= getElementByXPath(Hola)`  
* Y ahora puedo ir revisando los elementos con:  
`var un_hola= tienen_hola.iterateNext()`  
lo que devuelve (por ejemplo):  
`<span dir="ltr" class="_19RFN _1ovWX _F7Vk">Hola, buen dia</span>`  
Y le puedo pedir informacion como la clase, el texto, los nodes hijo y padres, etc.
  
* Cuando algo cambia en la pagina (ej: si llega un mensaje) se pierde la variable donde guardé el XPath, por lo que hay que llamar a la función de vuelta y volver a empezar las iteraciones.

## Ejemplo en WhatsApp:
```
function getElementByXPath(path) {
 return document.evaluate(path, document, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);
}

var tienen_hola= getElementByXPath('//*[text()[contains(.,"Hola")]]');
var un_hola= tienen_hola.iterateNext();
var message_class= un_hola.parentElement.parentElement.parentElement.parentElement.parentElement.parentElement.parentElement.classList[0]; //El texto con el 'Hola' esta metido dentro de muchos nodes hasta llegar al del mensaje entero.
var unsorted_messages= document.getElementsByClassName(message_class); //Ahora, dentro de message tengo todos los mensajes

function sortMessages(messages) {
    var r= {
      out:[],
      in:[],
    }
    
    for (var message of messages) {
        var class_name= message.className;
        if (class_name.includes('message-in')) {
            r.in.push(message);
        } else if (class_name.includes('message-out')) {
            r.out.push(message);
        }
    }
    
    return r
}

var sorted_messages= sortMessages(unsorted_messages); //Los separé entre enviados y recibídos
```
