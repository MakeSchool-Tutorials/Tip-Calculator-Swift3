---
title: "Tip it up!"
slug: adding-the-logic
---

## Linking your interface to code

_Xcode_ makes it easy to connect your interface to code. Now that we've got an interface let's get it hooked up to our code files!

>[info]
>
There are two main kinds of code connections: _outlets_, and _actions_.
>
> _Outlets_ let you assign a variable in code to a component of your interface you have created in your storyboard to interact with that component in code. _Outlets_ are very useful for objects such as text fields, because it means that we can change the text within the field in our Swift class, by modifying the variable that is directly linked to it.

> _Actions_ let you create a function in code that is called whenever a user interacts with a component of the interface. _Actions_ are great for buttons & segmented controls, because, for example, they tell our Swift class that the user has tapped that button with their finger.

<!--  -->

>[action]
> ## Adding code connections
>
1. Close the layout tree and attribute inspector to make some room.
1. Open the assistant editor and make sure `ViewController.swift` is displayed by switching from "Preview" to "Automatic" in the dropdown menu above the assistant editor view window.
1. Control-click (or right-click) drag from `bill amount text field` to under the `class ViewController` line and name the outlet `billAmountField`.
1. Control-click (or right-click) drag from the `tip selector segmented control` and name the outlet `tipSelector`.
1. Control-click (or right-click) drag from the `tip amount text field` and name the outlet `tipAmountField`.
1. Control-click (or right-click) drag from the `total amount text field` and name the outlet `totalAmountField`.
1. Control-click (or right-click) drag from the `calculate` button to the view controller. Choose `Action` and name it `calculateTip`.
1. Add some space to clean up the file.
>
> ![ms-video](https://s3.amazonaws.com/mgwu-misc/TipCalculator-Swift3/17_outlets_and_actions.mp4)

# Adding the logic

> [info]
>
> Before we get started with the logic, we need to go over a new Swift concept! Let's talk about `if let` statements...
>
> `if let` is a special statement that allows us to check the condition of a variable and perform actions based on that condition. In the code below, we are saying if you can cast `billAmount` to a `Double` and save it to  a new variable called `billAmount`, then do nothing. However, if you cannot do this, then we should stop what we are doing and clear the fields". If the condition _is_ met, then the function can continue.

Now that we have some _outlets_ and _actions_, we can actually code our logic. Since this tutorial is about _Xcode_, not programming, we are going to give you the logic. Study the code below and make sure you understand the logic!

> [action]
> Add the following to your `calculateTip` function. You should type it out and make sure you understand the logic!
>
```
if let billAmount = Double(billAmountField.text!) {
    var tipPercentage = 0.0
>
    switch tipSelector.selectedSegmentIndex {
    case 0:
        tipPercentage = 0.15
    case 1:
        tipPercentage = 0.18
    case 2:
        tipPercentage = 0.20
    default:
        break
    }
>
    let roundedBillAmount = round(100 * billAmount) / 100
    let tipAmount = roundedBillAmount * tipPercentage
    let roundedTipAmount = round(100*tipAmount)/100
    let totalAmount = roundedBillAmount + roundedTipAmount
>
    if (!billAmountField.isEditing) {
        billAmountField.text = String(format: "%.2f", roundedBillAmount)
    }
    tipAmountField.text = String(format: "%.2f", roundedTipAmount)
    totalAmountField.text = String(format: "%.2f", totalAmount)
} else {
    //show error
    billAmountField.text = ""
    tipAmountField.text = ""
    totalAmountField.text = ""
}
```
>
Run it and give it a spin! Do you understand the code? Hover over the _Solution_ below to see an explanation!

<!--  -->

> [solution]
> The `calculateTip` function starts off with a `if let` statement. If `billAmount` does not contain a number, it resets all of the fields.
>
> If it does have a number, then the function continues. It uses a `switch` statement to read the segmented control and set `tipPercentage`. It then calculates the `tipAmount` and `totalAmount`. Finally, it updates the respective text fields.

# Testing it out

Now that we have an interface, code connections, and logic... let's test it all out! Run the simulator and try calculating a tip :)

![ms-video](https://s3.amazonaws.com/mgwu-misc/TipCalculator-Swift3/18_testing_the_code.mp4)

# Quick Review

> Let's look at what you just did in this section:
>
1. Learned about code connections and the difference between an outlet and an action
1. Created Outlets for the Text Field objects
1. Created an Action for the calculate button
1. Added the logic into the class to make the buttons work
1. Tested out the app on our phones (or on the simulator) to ensure that everything is working
>
> Looking good! Everything seems to work. On the next page, we'll make some small UI improvements before moving on to a more substantial app!
