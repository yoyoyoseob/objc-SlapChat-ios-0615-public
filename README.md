---
  tags: tutorial, intermediate, CoreData, APIs, Blocks, Multi-threading
  languages: objc
---

Core Data SlapChat (patent pending)
=========

### Goals 
- Set up the Core Data Stack 
- Use UIImagePicker to take a photo or select a photo from your photo library
- Use UIActivityViewController for data sharing 
- Use Airdrop for local SlapChatting 

###Project Overview 

The goal behind this lab is to build the next Billion dollar App, SlapChat.  SlapChat turns the idea of anonymous photo-sending on its head by allowing you to save and share your precious photos. If anyone is interested in investing, we are accepting investments with a minimum of $100 million. 

#### Specifics

Upon launch, you'll land on a UITableView Controller.  The table view will load in an array of saved pictures from Core Data. Tapping on a cell will open a UIActivityViewController which will allow you to share your photo VIA text, or Email.  The navigation bar will have a + button which will transition open up a new `UIImagePickerController` that allows you to grab a photo. When someone selects a photo they are then brought back to the `UITableView` with the creation date and time (formatted "MM/dd/yyyy HH:mm").

### Instructions

  1. Make a new Project with a `UITableViewController` and a plus button for the right `UIBarButtonItem`
  2. Create a new class `FISMessage` that has two properties: date and image.
  3. Create a dataStore singelton. Add an `NSArray` property that will hold your `FISMessage` objects
  4. When the add button is tapped, a `UIImagePickerController` is brought up and the user selects an image
  5. When the image is selected a new `FISMessage` should be added to the `UITableView` with the new message.
  6. Ok so kill the app... Double tap on the home button and 


### Hints


##Location 

### Links 


