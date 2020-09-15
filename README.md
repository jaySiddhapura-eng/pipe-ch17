# Pipes

## Table of Contents  
* [Introduction](#Introduction)<br>
* [Pipe Usage](#Pipe-Usage)<br>
* [Parameterizing The Pipes ](#Parameterizing-The-Pipes)<br>
* [Chaining Multiple Pipes](#Chaining-Multiple-Pipes)<br>
* [Creating Custom Pipe](#Creating-Custom-Pipe)<br>

## Introduction

1. Pipes are built in feature of Angular
2. Pipes modify the output while rendering it
3. Although it does not change the actual variable in the .ts file

## Pipe Usage

1. Pipe followed by pipe symbol ``` |```

2. Syntax

   ~~~html
   {{propertyFromTSFile | defaultPipes}}
   
   Example: making the property string uppercase before rendering it on template
   {{serverInstanceType | uppercase}}
   
   Example: transform property into date before rendering it 
   {{server.started | date}}
   ~~~

## Parameterizing The Pipes 

1. Parameters can be added to the pipe by adding ```:```

2. Example: add parameter to the date pipe

   ~~~html
   {{server.started | date:'fullDate'}}
   parameter must be a string
   ~~~

3. Adding multiple parameters to the pipe by using ```:```

   ~~~html
   {{server.started | date : 'param1' : 'param2'}}
   ~~~

4. More resources about different kind of pipes : [Link](https://angular.io/api?query=pipe)

## Chaining Multiple Pipes

1. While chaining the pipe, order of the pipe is important

2. Application of the pipe on object starts from left to right

3. Example:

   ~~~html
   {{server.started | date : 'fullDate' | upperCase}}
   
   date pipe will apply first to the server.started property
   and then upperCase pipe will be applied to the above transformed proerty
   ~~~

## Creating Custom Pipe

1. Create a pipe which abbreviate the name when it applies to the property

   ~~~html
   {{server.started | shortner:2}}
   where 2 is parameter applies to the pipe shortner
   ~~~

2. Create a file ```shortner.pipe.ts``` in root

   ~~~typescript
   import { PipeTransform, Pipe } from "@angular/core";
   
   @Pipe({
       name: 'shorten'
   })
   export class ShortenPipe implements PipeTransform{
       
   	    transform(value: any, limit: number){
           	if(value.length > limit){
               	return value.substr(0, limit) + ' ...';
           	}
           	return value;
       	}
   }
   ~~~

3. Register this pipe in ```app.module.ts```

   ~~~typescript
   @NgModule({ 
       declarations: [ ShortenPipe ]
   })
   ~~~

   









