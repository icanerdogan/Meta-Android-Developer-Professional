## Building the app

## Project Planning

Project planning is an important part of commencing any new project. It serves as a roadmap that shows the phases of the project, as well as their start and end dates and dependencies.

Project planning is one of the most critical stages of software development. Let's explore why it's is so important.

## 1. Project performance and success rates

Project planning involves comprehensive mapping and organization of project goals, tasks, schedules and resources before anyone assigns project roles and the team starts implementing the plan. With proper planning in place, you can boost the project performance and success rates of a team.

## 2. Clear objectives

Having a clear direction of what needs to be achieved greatly increases the likelihood that you will do it. But without a concise objective from the start, the project will be complicated. If the team isn't clear on what they are working on, it’s almost impossible to know when the project is completed. Proper planning helps the team focus on the most important thing, the objectives and the end goal.

## 3. Resource allocation

Having a project planned out shows how much of the workforce is required to execute the project. The plan also allows project managers to monitor which resources have been allocated and thus avoid excessive allocation.

## 4. Communication

Planning aids communication, which will help every team member know what exactly is required of them ahead of time. A well-written plan will help you communicate key details, making it seamless for you and your entire team to complete specific tasks. Listening to their input and ideas is also a great way to achieve buy-in and foster the commitment of every team member.

## 5. Project-specific Training

Project planning ensures team members have the required technical know-how to execute the assigned tasks and identifies talent pipelines to provide an adequate supply of trained talents throughout the lifecycle of the project.

## Layouts

## What is a layout?

In Android, layout defines the user interface (UI) for an app or activity and holds the UI elements that will appear to the user.

Related to layouts are **View** and **ViewGroup**.

### View

A **View** is defined as the UI which is used to create interactive UI components such as **TextView**, **ImageView**, **Label**, **RadioButton** and so on. It is in charge of event handling and drawing. They are generally referred to as "widgets".

### ViewGroup

A **ViewGroup** serves as a parent class for layouts and layout parameters that hold other Views or ViewGroups and define the layout properties. They are generally referred to as "layouts".

## **Types of Android Layouts**

### **LinearLayout**

**LinearLayout** is a ViewGroup subclass used to render child View elements one after the other either horizontally or vertically based on the orientation property specified.

### **ConstraintLayout**

**ConstraintLayout** is a ViewGroup subclass used to specify the position of layout constraints for every child View relative to other views on the screen.

### **Frame Layout**

**FrameLayout** is a ViewGroup subclass used to specify the position of View elements it contains on the top of each other to display only a single View inside the **FrameLayout**.

### **Table Layout**

**TableLayout** is a ViewGroup subclass used to display the child View elements in rows and columns.

### **WebView**

**WebView** is a browser that is used to display the web pages in your activity layout.

### **RecyclerView**

You can use **RecyclerView** with LinearLayoutManager to display scrollable lists of items in a single column. You can also use **RecyclerView** with GridLayoutManager to display a scrollable list of items in a grid view of rows and columns.

## Views

## What are Views?

The View object is created from the View class and occupies a rectangular screen area. It is responsible for the processing of drawings and events.

The View is the base class for widgets that are used to create interactive components of the user UI such as buttons or text fields.

In summary, a View can be considered a rectangle on the screen that displays a certain type of content, like an image, a piece of text or even a button!

## Most used Android Views

Some of the most used Android Views include:

- TextView
- EditText
- Button
- ImageView
- ImageButton
- CheckBox
- RadioButton
- RecyclerView
- DatePicker and
- Spinner

## View sizes

A View occupies a rectangle shape, although the rectangle is invisible.

The size of this rectangle can be manually set by specifying the exact size (with appropriate units) or using some predetermined values. These predefined values are **match_parent** and **wrap_content**.

**match_parent** means it will occupy all of the available space available within its parent ViewGroup, whereas **wrap_content** means it will occupy only as much space as required for its content to display.

## XML syntax for creating a View

Now, as you learned previously, to draw anything in your Android application you need to specify it in the design XML files. You will create Kotlin files to add functionality.

Every View in XML has the following format:

```jsx
<ViewName
    Attribute1=Value1
    Attribute2=Value2
    Attribute3=Value3
    AttributeN=ValueN
/>
```

- It always starts with an angle bracket, followed by the View name.
- You then write attributes that will determine what this view will look like on the app screen along with a value for the attribute. Each view has its own unique attributes.
- In the end, it is closed by a forward slash and an angle bracket.

So, every View subclass needs to follow this standard so that it can display on the screen of the app. This format is the default standard of XML.

Take note that there are two attributes that are required for every View. These are **android:layout_height** and **android:layout_width**.

These attributes determine the size of the invisible rectangle created by the view. Using these attributes, you control the size of every view in your Android app.

> **[Android layouts and XML](https://developer.android.com/develop/ui/views/layout/declaring-layout)**
>

> **[ExoPlayer in Android](https://developer.android.com/guide/topics/media/exoplayer)**
>

> **[Kotlin](https://kotlinlang.org/docs/basic-syntax.html#functions)**
>

> **[VideoView Class](https://developer.android.com/reference/android/widget/VideoView)**
> 
