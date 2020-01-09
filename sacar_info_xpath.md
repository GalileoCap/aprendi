# Sacar información de paginas web usando XPath
## Descripcion
* Puedo buscar entre los elementos usando la función:  
`function getElementByXPath(path) {`  
` return document.evaluate(path, document, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);`  
`}`
* Por ejemplo, si quiero buscar todos los elementos que contengan la palabra "Hola", la llamo con el path= '//*[text()[contains(.,"Hola")]]' y la guardo en una variable  
`var hola= '//*[text()[contains(.,"Hola")]]';`  
`var tienenHola= getElementByXPath(hola)`  
* Y ahora puedo ir revisando los elementos con:  
`var unHola= tienenHola.iterateNext()`  
lo que devuelve (por ejemplo):  
`<span dir="ltr" class="_19RFN _1ovWX _F7Vk">Hola, buen dia</span>`  
Y le puedo pedir informacion como la clase, el texto, los nodes hijo y padres, etc.
  
* Cuando algo cambia en la pagina (ej: si llega un mensaje) se pierde la variable donde guardé el XPath, por lo que hay que llamar a la función de vuelta y volver a empezar las iteraciones.

## Ejemplo en WhatsApp:
```
function getElementByXPath(path) {
 return document.evaluate(path, document, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);
}
var tienenHola= getElementByXPath('//*[text()[contains(.,"Hola")]]');
var unHola= tienenHola.iterateNext();
var a= unHola.parentElement.parentElement.parentElement.parentElement.parentElement.parentElement.parentElement; //El texto con el 'Hola' esta metido dentro de muchos nodes hasta llegar al del mensaje entero.
var b= a.classList[2];
var c= document.getElementsByClassName(b); //Ahora, dentro de C tengo todos los mensajes
```
