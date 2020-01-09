# Sacar información de paginas web usando XPath
* Puedo buscar entre los elementos usando la función:  
`function getElementByXPath(path) {`  
` document.evaluate(path, document, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);`  
`}`
* Por ejemplo, si quiero buscar todos los elementos que contengan la palabra "Hola", la llamo con el path= '//*[text()[contains(.,"Hola")]]' y la guardo en una variable  
`var hola= '//*[text()[contains(.,"Hola")]]';`  
`var tienenHola= getElementByXPath(hola)`  
* Y ahora puedo ir revisando los elementos con:  
`var unHola= a.iterateNext()`  
lo que devuelve (por ejemplo):  
`<span dir="ltr" class="_19RFN _1ovWX _F7Vk">Hola, buen dia</span>`  
Y le puedo pedir informacion como la clase, el texto, los nodes hijo y padres, etc.
