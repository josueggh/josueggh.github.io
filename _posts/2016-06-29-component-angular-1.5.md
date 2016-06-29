---
layout: post
title: Método .component() en Angular 1.5
subtitle: Código modular y más fácil de implementar
categories: [angular, component, post]
---

Desde el último release estable de Angular(1.5.0), se introdujo el método de **.component()**, el cuál nos permite simplificar la manera en que creamos directivas y que en cierta manera nos permite escribir código pensando en la versión de Angular 2.

A diferencia de la directiva, la cual era generada a partir de una función, un componente permite definir su comportamiento a partir de un objeto.

```javascript
/*Directiva*/
.directive('hello', function(){
  return {
    scope : {},
    bindToController:{
      name : '='
    },
    controller: function(){}
    controllerAs: 'helloCtrl',
    template: '<h1>Hello {{helloCtrl.name}}</h1>'
  }
});

/*Component*/
.component('hello', {
  bindings: {
    name: '='
  },
  template: '<h1>Hello {{$ctrl.name}}</h1>'
})
```
Entre las primeras diferencias que notamos se encuentra la manera en que obtenemos los atributos de nuestros elementos, nuestra directiva utiliza **bindigToController** el cual fu simplificado a **bindings**, de está manera nuestro componente obtiene los valores directamente.

```javascript
/*Drectiva*/
  bindToController:{
    name: '='
  },

/*Component*/
  bindings: {
    name: '='
  },
```
El siguiente cambio que notamos, es que no tenemos la necesidad de incluir **controller** y **controllerAs** de primera instancia en la definición de nuestro componente, esto se debe a que dentro de nuestro componente ahora existen valores de default para cada uno de estros atríbutos de nuestro objeto:

```javascript
/*Directiva*/
    controller: function(){}
    controllerAs: 'helloCtrl',
    template: '<h1>Hello {{helloCtrl.name}}</h1>'
 
/*Component*/
  template: '<h1>Hello {{$ctrl.name}}</h1>'
```

Internamente los valores que tiene Angular para el componente son los siguientes:

|              | directive      | component             |
|--------------|----------------|-----------------------|
| controller   | default:None   | default: function(){} |
| controllerAs | default: false | default: $ctrl        |

Algo que debemos de tener en cuenta es que todos nuestros componentes funcionan con el valor de restrict **E**, por lo que siempre será necesario llamarlos como elementos dentro de nuestro HTML, si necesitamos modificar el DOM o crear elementos a partir de clases o atributos es necesario utilizar una directiva para mantener correcta la arquitectura de nuestra aplicación.