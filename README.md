# About

<a href="https://ionic-6-ts-back4app-todolist-andgoedu.netlify.app">Demo</a>

An ionic 6 , web application built in typescript and react js framework ,while in terms of the backend back 4app was used as the api .

- Start By
- ```yarn install```
- ADD Api keys from [parse dashboard back4app](https://parse-dashboard.back4app.com/)
- 1. Select your application or create a new one
  
- 1.1 - Make ACLS public . Note this is not recommended for deployment only development
  
- 2. Go to App settings on the left
  
- 3. Select security and keys and get the api keys

```.env
REACT_APP_PARSE_ID=
REACT_APP_PARSE_HOST_URL=
REACT_APP_PARSE_JS_KEY=
```

- After these simple steps Serve application and Enjoy !
  
## Start By 🚀

```
ionic serve
```

- Project Built With

## Project Requirements

1. [nodejs 16.18.0](https://nodejs.org/en/)

Make sure you installed node and node package manager using ```npm -v``` and ```node -v```

2. [yarn](https://yarnpkg.com/)
  
- Install yarn by using
  
```

npm install -g yarn

```

3. [ionic framework](https://ionicframework.com/getting-started)

```

npm i -g @ionic/cli

```

## Setup the project

```ts
ionic start todoApp --type=react --capacitor
```

-- use yarn instead of npm
```ionic config set -g yarn true```

### Packages to install

`parse` From [parse  - yarn pkg](https://yarnpkg.com/package/parse)
``` @parse/react ``` From [@parse/react - yarn pkg](https://yarnpkg.com/package/@parse/react)

& [Getting started with the Parse React hook for real time updates using Parse](https://www.back4app.com/docs/react/real-time/react-hook-real-time)

```
yarn add @parse/react parse
```

#### Setup BackEnd Schema

```ts
// Step 1 Add Parse API Keys into App.tsx
//  Require Parse for tsx
const Parse = require('parse');

// Step 1 Your Parse initialization configuration goes here
const PARSE_APPLICATION_ID = ' ';
const PARSE_HOST_URL = 'https://parseapi.back4app.com/';
const PARSE_JAVASCRIPT_KEY = ' ';

```

##### Project Structure and files to add

```
- public
- /assets               // images
-  /icons               // favicon.ico for example
- index.html            // the html rendered webpage
- src                   //root folder
- /components           // where all the components reside
-  /CreateToDo          //1. create new folder inside ./src/components/ call it CreateToDo
-  /CreateToDo.tsx      //2.  create new file inside /src/components/CreateToDo call it CreateToDo.tsx 
- /pages                //where all pages reside
-  /EditToDo            //3.create new folder inside ./src/pages/ call it EditToDo
-  /EditToDo.tsx        //4. create new file inside ./src/pages/EditToDo call it EditToDo.tsx 
- /theme                // Where ionic app.css styles reside
-   /variables.css      // ionic default css variables for dark or light mode
- App.tsx               // Where the application component resides, the ionic router and also initializeParse Client
- index.tsx             // Where the application renders in the index.html <div id="root" ></div>  
- .env                  // Where all the Api Keys are going to be saftely stored for production

```

1. CREATE [x]

```ts
// ADD IMPORTS 
import React, { useState, useEffect } from "react";
import {
  IonCol,
  IonLabel,
  IonInput,
  IonTextarea,
  IonButton,
  IonIcon,
  IonGrid,
  IonRow,
  IonItem,
  IonText,
} from "@ionic/react";

import { add,paperPlaneOutline } from "ionicons/icons";

const Parse = require("parse");

// Export a default function 

export default function CreateToDo() {

    return (
        <></>
    )
    }
```

```tsx
 //ADD STATE VAR AND STATE ACTION AND ASSIGN PROPERTIES
  const [newToDoObject, setNewToDoObject] = useState({
    title: "",
    description: "",
    task: "",
    isCompleted: false,
    createdAt: new Date(),
    updatedAt: new Date(),
  });
```

```tsx
//ADD async arrow function to handle creating the new to object{}

 const createNewToDoObject = async () => {
    const newToDo = new Parse.Object("ToDo", newToDoObject);
    newToDo.set(newToDoObject);

    try {
      const newToDoObject = await newToDo.save();

      const newToDoObjJSON = JSON.stringify(newToDoObject);

      alert("The New To Do Object Has been Created >>>>! " + newToDoObjJSON);
    } catch (error: any) {
      alert("Errro was found in createNewToDoObject " + error);
    }
  };
```

```tsx

//Hanlde ToDoChg 

const handleToDoCHG= (event: any)=> {

setNewToDoObject((previous : any)=> ({
  ...previous,
  [event.target.name]: event.target.value,
}));

//html5

};
```

- Make sure to match the html5 property name with the properties passed to the object
- Also add ```onIonChange={handleToDoCHG}``` in each input to handle the users input

```tsx
//ADD html5 name property and handleToDoCHG to handle the user inputs change 
<IonGrid fixed={true}>
  <IonText>
  Create ToDo <IonIcon icon={paperPlaneOutline}/>
  </IonText>

    <IonInput name="title" onIonChange={handleToDoCHG} placeholder="Enter Title here..." maxlength={25}/>
  
      <IonInput name="task" onIonChange={handleToDoCHG} placeholder="Enter Task here..." maxlength={25} />

 
      <IonTextarea name="description" onIonChange={handleToDoCHG} style={{resize: "none"}} placeholder="Enter Description here..."  maxlength={100}/>


<IonButton onClick={createNewToDoObject} expand="block" color={"success"}> <IonIcon icon={add} />
</IonButton>
</IonGrid>

```

Final File CreateToDo.tsx

```tsx
//CreateToDo.tsx
import React, { useState, useEffect } from "react";
import {
  IonCol,
  IonLabel,
  IonInput,
  IonTextarea,
  IonButton,
  IonIcon,
  IonGrid,
  IonRow,
  IonItem,
  IonText,
} from "@ionic/react";

import { add, paperPlaneOutline } from "ionicons/icons";

const Parse = require("parse");

export default function CreateToDo() {
  //STATE VAR AND STATE ACTION AND ASSIGN PROPERTIES
  const [newToDoObject, setNewToDoObject] = useState({
    title: "",
    description: "",
    task: "",
    isCompleted: false,
    createdAt: new Date(),
    updatedAt: new Date(),
  });

  const createNewToDoObject = async () => {
    const newToDo = new Parse.Object("ToDo", newToDoObject);
    newToDo.set(newToDoObject);

    try {
      const newToDoObject = await newToDo.save();

      const newToDoObjJSON = JSON.stringify(newToDoObject);

      alert("The New To Do Object Has been Created >>>>! " + newToDoObjJSON);
    } catch (error: any) {
      alert("Errro was found in createNewToDoObject " + error);
    }
  };

  //Hanlde ToDoChg

  const handleToDoCHG = (event: any) => {
    setNewToDoObject((previous: any) => ({
      ...previous,
      [event.target.name]: event.target.value,
    }));

    //html5
  };

  return (
    <>
      <IonGrid fixed={true}>
        <IonText>
          Create ToDo <IonIcon icon={paperPlaneOutline} />
        </IonText>
        <IonRow>
          <IonCol size="6">
            <IonItem>
              <IonLabel color={"success"} position="stacked">
                Title
              </IonLabel>
              <IonInput
                name="title"
                onIonChange={handleToDoCHG}
                placeholder="Enter Title here..."
                maxlength={25}
              />
            </IonItem>
          </IonCol>

          <IonCol size="6">
            <IonItem>
              <IonLabel color={"success"} position="stacked">
                Task
              </IonLabel>
              <IonInput
                name="task"
                onIonChange={handleToDoCHG}
                placeholder="Enter Task here..."
                maxlength={25}
              />
            </IonItem>
          </IonCol>

          <IonCol size="10">
            <IonItem>
              <IonLabel color={"success"} position="stacked">
                Description
              </IonLabel>
              <IonTextarea
                name="description"
                onIonChange={handleToDoCHG}
                style={{ resize: "none" }}
                placeholder="Enter Description here..."
                maxlength={100}
              />
            </IonItem>
          </IonCol>

          <IonCol size="2">
            <IonButton
              onClick={createNewToDoObject}
              expand="block"
              color={"success"}
            >
              {" "}
              <IonIcon icon={add} />
            </IonButton>
          </IonCol>
        </IonRow>
      </IonGrid>
    </>
  );
}
```

2. READ []

```tsx
//1. STATE VAR And SetStateAction
  var [toDos, setToDos] = useState([
    {
      objectId: " ",
      title: "",
      description: "",
      task: "",
      isCompleted: Boolean(),
      createdAt: new Date(),
      updatedAt: new Date(),
    },
  ]);




```

```tsx
 // extending the Parse object
  const ToDo: Parse.Object[] = Parse.Object.extend("ToDo"); // extend todo

  const parsequery: Parse.Query = new Parse.Query(ToDo);

```

```tsx
  //2. ASYNC Function to handle reading tasks with useCallback hook to handle each task instead of going in an infinte loop
  const readTasks = useCallback(async function (): Promise<Boolean> {
    try {
      const results: Parse.Object[] = await parsequery.find();

      const mappedData = [];

      for (const object of results) {
        const objId: string = object.id;
        const title: string = object.get("title");
        const decription: string = object.get("description");
        const task: string = object.get("task");
        const isCompleted: boolean = object.get("isCompleted");
        const createdAt: Date = object.get("createdAt");
        const updatedAt: Date = object.get("updatedAt");

        let resultsFix = {
          objectId: objId, //string
          title: title, //string
          description: decription,
          task: task,
          isCompleted: isCompleted, //boolean
          createdAt: createdAt, //date
          updatedAt: updatedAt, //date
        };

        mappedData.push(resultsFix);
      }
      setToDos(mappedData);
      return true;
    } catch (error: any) {
      console.warn("Error has been found in readTasks " + error);
      return false;
    }
  }, []);

  console.log(toDos);
```

```tsx
  // 3. useEffect
  useEffect(() => {
    readTasks();
    //uncomment these lines after addint the refreshTasks async arrow function
    //refreshTasks();
  }, [readTasks, /*refreshTasks*/]);
  ```

3. UPDATE []

```tsx
    //UPDATE TODO

        const completeTask = async () => {
          try {
            const object = await parsequery.get(objId);
            object.set("isCompleted", true);
            object.set("objectId", objId);
            object.save();
          } catch (error: any) {
            console.warn("Error has been found in completeTask" + error);
          }
        };

```

4. DELETE []

```tsx
   //DELETE TODO
        const deleteToDo = async () => {
          try {
            const singleObject: Parse.Object = await parsequery.get(objId);

            const response: any = await singleObject.destroy();

            if (response) {
              alert(`${objId} To Do Has Been Deleted`);
            } else {
              alert(`Error: Nothing was Delted`);
            }

            return true;
          } catch (error: any) {
            console.warn("Error has been found in deleteToDo" + error);
          }
        };

```

5. Refresh Tasks

```tsx
 /*-------------< TODO REFRESH TASKS START >---------*/
  const refreshTasks = useCallback(
    async function () {
      var query = new Parse.Query("ToDo");
      query
        .find()
        .then((results: Parse.Object) => {
          //DEBUG
          //Stringified Value of Results
          //const resultsStr = JSON.stringify(results);
          //console.log("Results of ToDo parse Object is >>>" + resultsStr);
          //
        })
        .then(() => {
          query.count().then((ToDoCount: Number) => {
            console.log("Number of tasks is = " + ToDoCount);
          });
        })
        .catch((error: any) => {
          // error is an instance of parse.error.
          console.log(error);
        });
      //REFRESH TASKS TO REMOVE THE DELETED ONES ID
      readTasks();
      return true;
    },
    [readTasks]
  );
  /*-------------< TODO REFRESH TASKS END >---------*/

```

Final File in ./src/components/EditToDo/EditToDo.tsx

```tsx
import React from "react";
import {
  IonButton,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCol,
  IonIcon,
  IonItem,
  IonText,
  IonCheckbox,
  IonBadge,
  IonRippleEffect,
  IonRow,
  IonGrid,
} from "@ionic/react";

import { close, returnDownBack } from "ionicons/icons";

import { FC, ReactElement, useCallback, useEffect, useState } from "react";

const Parse = require("parse");

const EditToDo: FC<{}> = (): ReactElement => {
  //1. STATE VAR And SetStateAction
  var [toDos, setToDos] = useState([
    {
      objectId: " ",
      title: "",
      description: "",
      task: "",
      isCompleted: Boolean(),
      createdAt: new Date(),
      updatedAt: new Date(),
    },
  ]);

  // extending the Parse object
  const ToDo: Parse.Object[] = Parse.Object.extend("ToDo"); // extend todo

  const parsequery: Parse.Query = new Parse.Query(ToDo);

  //2. ASYNC Function to handle reading tasks with useCallback hook to handle each task instead of going in an infinte loop
  const readTasks = useCallback(async function (): Promise<Boolean> {
    try {
      const results: Parse.Object[] = await parsequery.find();

      const mappedData = [];

      for (const object of results) {
        const objId: string = object.id;
        const title: string = object.get("title");
        const decription: string = object.get("description");
        const task: string = object.get("task");
        const isCompleted: boolean = object.get("isCompleted");
        const createdAt: Date = object.get("createdAt");
        const updatedAt: Date = object.get("updatedAt");

        let resultsFix = {
          objectId: objId, //string
          title: title, //string
          description: decription,
          task: task,
          isCompleted: isCompleted, //boolean
          createdAt: createdAt, //date
          updatedAt: updatedAt, //date
        };

        mappedData.push(resultsFix);
      }
      setToDos(mappedData);
      return true;
    } catch (error: any) {
      console.warn("Error has been found in readTasks " + error);
      return false;
    }
  }, []);

  console.log(toDos);

  /*-------------< TODO REFRESH TASKS START >---------*/
  const refreshTasks = useCallback(
    async function () {
      var query = new Parse.Query("ToDo");
      query
        .find()
        .then((results: Parse.Object) => {
          //DEBUG
          //Stringified Value of Results
          //const resultsStr = JSON.stringify(results);
          //console.log("Results of ToDo parse Object is >>>" + resultsStr);
          //
        })
        .then(() => {
          query.count().then((ToDoCount: Number) => {
            console.log("Number of tasks is = " + ToDoCount);
          });
        })
        .catch((error: any) => {
          // error is an instance of parse.error.
          console.log(error);
        });
      //REFRESH TASKS TO REMOVE THE DELETED ONES ID
      readTasks();
      return true;
    },
    [readTasks]
  );
  /*-------------< TODO REFRESH TASKS END >---------*/

  // 3. useEffect
  useEffect(() => {
    readTasks();
    refreshTasks();
  }, [readTasks, refreshTasks]);

  return (
    <>
      <IonRow>
        <IonCol size="10">
          <IonButton onClick={refreshTasks} color="secondary" expand="block">
            <IonIcon icon={returnDownBack} />
          </IonButton>
        </IonCol>

        <IonCol size="2">
          <IonBadge color={"medium"}>{toDos?.length}</IonBadge>
        </IonCol>
      </IonRow>

      {toDos?.map((todo: any, index: any) => {
        // MAP OVER THE TODOS AND RETURN THE INFO

        //GET ID

        var objId: string = todo?.objectId;
        //console.log(objId);

        //DELETE TODO
        const deleteToDo = async () => {
          try {
            const singleObject: Parse.Object = await parsequery.get(objId);

            const response: any = await singleObject.destroy();

            if (response) {
              alert(`${objId} To Do Has Been Deleted`);
            } else {
              alert(`Error: Nothing was Delted`);
            }

            return true;
          } catch (error: any) {
            console.warn("Error has been found in deleteToDo" + error);
          }
        };

        //UPDATE TODO

        const completeTask = async () => {
          try {
            const object = await parsequery.get(objId);
            object.set("isCompleted", true);
            object.set("objectId", objId);
            object.save();
          } catch (error: any) {
            console.warn("Error has been found in completeTask" + error);
          }
        };

        return (
          <div key={todo + index}>
            <IonGrid fixed={true}>
              <IonRippleEffect></IonRippleEffect>

              <IonCard color={todo.isCompleted === true ? "success" : "medium"}>
                <IonCardHeader
                  color={todo?.isCompleted === true ? "light" : "warning"}
                >
                  <IonRow>
                    <IonCol size="9">
                      <IonText
                        color={todo?.isCompleted === true ? "dark" : "light"}
                      >
                        <h5>{[todo?.title?.toLocaleUpperCase() || " "]}</h5>
                      </IonText>
                    </IonCol>
                    <IonCol size="3">
                      <IonButton
                        color="danger"
                        expand="block"
                        onClick={deleteToDo}
                      >
                        <IonIcon icon={close} />{" "}
                      </IonButton>
                    </IonCol>
                  </IonRow>
                </IonCardHeader>

                <IonItem
                  color={todo?.isCompleted === true ? "success" : "medium"}
                >
                  <IonText color={"light"}>
                    Task :{[todo?.task?.toLocaleLowerCase() || " "]}
                  </IonText>
                </IonItem>

                <IonCardSubtitle className="ion-text-center">
                  <h5 className="ion-text-white">
                    <strong>Description</strong>
                  </h5>
                  <em>{[todo?.description?.toLocaleLowerCase() || " "]}</em>
                </IonCardSubtitle>

                <IonCardContent>
                  <IonRow>
                    <IonCol size="10">
                      <table>
                        <thead>
                          <tr>
                            <th>Task</th>
                            <th>Completed</th>
                            <th>CreatedAt</th>
                            <th>updatedAt</th>
                          </tr>
                        </thead>

                        <tbody>
                          <tr>
                            <td> {todo?.task}</td>
                            <td>
                              {" "}
                              <IonCheckbox
                                color="medium"
                                // eslint-disable-next-line react/jsx-no-duplicate-props
                                onClick={completeTask}
                                disabled={todo?.isCompleted === true}
                              />{" "}
                              {todo?.isCompleted.toLocaleString()}
                            </td>
                            <td> {todo.createdAt?.toDateString()}</td>
                            <td> {todo.updatedAt?.toDateString()}</td>
                          </tr>
                        </tbody>
                      </table>
                    </IonCol>
                  </IonRow>
                </IonCardContent>
              </IonCard>
            </IonGrid>
          </div>
        );
      })}
    </>
  );
};

export default EditToDo;


```

###### References

1. [Signing up in Parser - Back4App Docs](https://dashboard.back4app.com/apidocs/2gaA8FOymlxMuiFxPnGvzaDNDuNe1DOK31ytUZGi?typescript#signing-up)
2. [Logging Page in Parser -  Back4App Docs](https://dashboard.back4app.com/apidocs#logging-in)
3. [How TO - Responsive Text W3Schools](https://www.w3schools.com/howto/howto_css_responsive_text.asp)
4. [User Password Reset for React Parse -  Back4App Docs](https://www.back4app.com/docs/react/working-with-users/react-password-reset)
5. [Theming Basics Ionic-framework Colors](https://ionicframework.com/docs/theming/basics)
6. [Theming Basics Ionic-framework Colors customziation](https://ionicframework.com/docs/theming/colors)
7. [aaronksaunders-ionic-react-tabs-side-auth](https://github.com/aaronksaunders/ionic-react-tabs-side-auth)
8. [Stringify a JavaScript Array](https://www.w3schools.com/js/js_json_stringify.asp)
9. [GitHubMapBoxLanguage](https://github.com/mapbox/mapbox-gl-language/)
10. [Map-Box Ar Example](https://mapbox.github.io/mapbox-gl-language/examples/ar.html#3/38.88/-98)
11. [CodePen HomeChange a map's language](https://codepen.io/pen)
12. [Parse~ ParseQuery](https://parseplatform.org/Parse-SDK-JS/api/master/Parse.Query.html)
13. [use-react-memo-wisely/](https://dmitripavlutin.com/use-react-memo-wisely/)
14. [React.memo](https://reactjs.org/docs/react-api.html#reactmemo)
15. [Migrating from npm](https://classic.yarnpkg.com/lang/en/docs/migrating-from-npm/)
16. [Colors - Ionic](https://ionicframework.com/docs/theming/colors)
17. [Parse JS Guide](https://docs.parseplatform.org/js/guide/)
18. [Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)
19. [react-chat-app - Back4App Docs](https://www.back4app.com/docs/react/real-time/react-chat-app)
20. [React CRUD tutorial - Back4App Docs](https://www.back4app.com/docs/react/data-objects/react-crud-tutorial)
21. [Ionic - Inputs](https://ionicframework.com/docs/api/input)
22. [Ionic - IonCheckBox](https://ionicframework.com/docs/api/checkbox)
23. [Ionic - ion-radio](https://ionicframework.com/docs/api/radio)
24. [this operator js - MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
25. [Ionic -ion-grid](https://ionicframework.com/docs/api/grid)
26. [Does not provide a valid apple-touch-icon](https://web.dev/apple-touch-icon/)
27. [Ionic -React Navigation](https://ionicframework.com/docs/react/**navigation**)
28. [ReactJs - useCallback hook](https://reactjs.org/docs/hooks-reference.html#usecallback)
29. [Using Yarn Instead of Npm for Ionic #10647](https://github.com/ionic-team/ionic-framework/issues/10647)

2.

Omar Zeinhom . AKA ANDGOEDU 2022-2023
