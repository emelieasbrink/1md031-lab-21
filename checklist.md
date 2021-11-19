# Checklist

Before you submit the final version of your labs, make sure that your project fullfills all of the tasks that will be added to this checklist.

## 00 Introduction

- [done] Install an IDE on your system

## 01 Git

- [done] Fork and clone the 1md031-lab-21 repository

## 02 HTML

Your index.html file contains:
- [done] A headline
- [done] A section to select burgers that contains at least three items. Each item has:
    - [done] A name
    - [done] An image
    - [done] Information about allergies
- [done] A section to collect customer information:
    - [done] First- and Last Name (in one field)
    - [done] E-Mail Address
    - [done] Street
    - [done] House Number (only allowing numbers in this field)
    - [done] Gender (male, female, do not wish to provide as radio buttons)
- [done] A button to place the order
- [done] Ensure the website loads when opening http://localhost:8080/

## 03 CSS

The style.css file contains:
- [done] A rule to make the allergy information bold
- [done] Different text and background color for the two different sections (burger selection and customer information)
- [done] Change the cursor when hovering over the order button
- [done] Adds margins to the sections and the order button
- [done] Add a border to the two sections
- [done] Create a header that places an image behind the headline
- [done] Use a grid layout for the burger selection section

## 04 JavaScript and Vue

- [ ] You have a menu.json file which contains at least three different burgers with respective attributes

Your Home.vue file:
- [done] ... contains a MenuItem constructor (that is not used)
- [done] ... loads the information from the menu.json object and inserts the information to the burger selection section
- [done] ... allows the customer to click in the interactive map to select delivery location
- [done] ... has an order button that sends the information from the text boxes, the gender, all items on the order, and the delivery location to the server (to be realyed to the dispatcher)

Your Burger.vue component:
- [done] ... allows adding and removing burgers from the order
- [done] ... only displays allergy information if relevant (either only if it contains gluten or lactose, or only if it's gluten or lactose free)

Your Dispatcher.vue file:
- [ ] ... shows for every order :
    - [done] a location on the map
    - [done] the order information
    - [done] the customer information
