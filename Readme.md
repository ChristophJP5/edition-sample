## Create a custom edition for FLOWFACT
First of all it is necessary to understand what an edition is. An edition consists of different things
that define a part of your workspace. For example the Commercial edition contains the schemas and views 
that are needed to create commercial estates and use them in flowfact correctly.

Let's create a custom edition as a sample together to get an understanding of how it works.
In this case, let's create a custom edition for a pet-shop.

First of all we create the folder that represents the edition. Name the folder like
the edition your going to create. In our case "petshop". To declare that this folder
is a flowfact-edition we need to create an empty ".bundle" file. This file indicates that
this folder is an edition and doesn't need to have any content. 

After that we create a details.json file in the folder. The details.json file defines 
who the creator of the edition is, how the edition is named and contains a description
for the edition.

The pet-shop will sell pets and foods for them. Since we want to track our customer-relation
for the things that we sell we'll need to create a bom.json. 
In this file we define that this edition requires that the edition "CRM" is installed. We also
define that customers will be able to install that edition manually.

After that we create a folder which is called "schemas". This folder will contain the pets
and the food as schemas that we have in our system. For each schema we create a folder which
is named like the schema we want to create. In our case we create a folder "pets" and a folder
"pet_foods".

Know the definition of the schemas can start.
First of all let's define which values the pets that we want to create in the system will have.

We need to think about which fields we need, how we want to name them, and which value type
they should store. For our pets it will look like this :

Fieldname | Type | Description | internal name
--------- | ---- | ----------- | -------------
ID | text | The id of the entity | identifier
Name | text | Name of the pet | name
Type | List | For example dog,cat,mouse | type
Age | Number | Age of the pet | age
Birthdate | Date | Birthdate of the pet | birthdate
Size | Unit - Number | Size of the pet | size
Healthcheck | Checkbox | If the pet is healthchecked | healthcheck
NewOwner | Schema-Link to contact | The new Owner of the pet | newowner
Sold | Checkbox | If the pet is already sold | sold
Picture | Media - Image | Picture of the pet | picture
Youtube Link | Link | For some pets we will make a short video to present them. | ytlink
Documents | Media - Documents | Things like selling contract | documents
Description | Textarea | Detailed description to the pet | description

The internal name is necessary to define in a way that is good to remember, because we need it
to define how our entities will be displayed in the client.

As for the Food that we're going to sell as a petshop we create a "pet_foods" folder and in there
a schema.json for it with the following values:

Fieldname | Type | Description | internal name
--------- | ---- | ----------- | -------------
ID | text | The id of the entity | identifier
Name | text | Name of the pet food | name
Type | List | For example dog,cat,mouse - food | type
Expiration Date | Date | Expiration Date of the food | expiration
Price | Unit - Number | Price of the food | price
Stock | Checkbox | If the food is in stock | stock
Deliverer | Schema-Link to contact | The deliverer | deliverer
Picture | Media - Image | Picture of the pet | picture
Purchase Link | Link | Link to purchase more of the food. | pclink
Description | Textarea | Detailed description to the pet | description

So we created the schemas for our pets and the food that we're going to sell. But at the moment,
we have no way defined of how we want to display the entities that will be created based on those
schemas. To create a possibility that the entities can be displayed in the client, we need 
to create views that the client uses to display the data.

There are 4 different Views that the client currently uses to display data:

* The "schema" view that defines how an entity will be displayed completely. All fields should be
displayed here.
* The "EntityRelationView" that defines how the entity will be displayed in a view when it can be
choosen as a link for a different entity.
* The "list" which defines which data should be displayed in a list.
* The "card" which defines which data should be displayed in the cards section.

You should at least create those 4 Views for every schema in your edition that you want to display
in the client.

To keep our example short at this point i'll link how the view.json files for the pets schema
will look like :

* pets
* EntityRelationView
* list
* card

I've also created the same files for the pet_foods schema. In the end of this Section i'll
also present a link to a Github page which contains the PetShop-Edition as a boilerplate
project to create new editions.

It is also possible to define more things for our schemas like widgets, and integrations but those
will be covered later.

The next step for our edition should be creating new Flywheels and Kanbans that can be used for
the schemas. In our sample we'll create a Pets-Flywheel only which consists of 3 Kanbans:

The Akquisition Kanban,The CareTaking Kanban and the Selling Kanban.
Each Kanban consists of its own phases. Kanbans and Flywheels have there own folder which
exists outside of the schema folder. So we need to go back to our main folder (where the details.json is located)
and create a new folder "kanbans" and a new folder "flywheels".

As i already said, our Flywheel will consist of 3 kanbans, so we create 3 json files inside
the kanban folder which look like those 3:

* kanban-1
* kanban-2
* kanban-3

Each children object in the kanban files represents one step in the kanban, so it's pretty
simple.

After we created the kanban files we need to create the flywheel file which now references to
the names of the kanbans that it consists of (the order is important here!).

flywheel-1

Create those files for your edition and you have created your first edition! 

Know you need to Zip the folder that contains all data and push it to FLOWFACT via the
Bundle-Upload API. Since this API is not documented at the moment but will follow shortly
send a mail to besnik.celaj@flowfact.de and i'll upload your edition.
