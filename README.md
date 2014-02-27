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

The goal behind this lab is to build the next Billion dollar App, SlapChat.  SlapChat turns the idea of anonymous photo-sending on its head by allowing you to save and share your precious photos. You'll create a CoreData Data store to save your pictures.  You'll use UIImagePicker to take a new photo or use an already saved photo and UIActivityViewController to share your photo.  

###Directions 

Upon launch, you'll land on a UITableView Controller.  The table view will load in an array of saved pictures from Core Data. Tapping on a cell will open a UIActivityViewController which will allow you to share your photo VIA text, or Email.  The navigation bar will have a + button which will transition to a viewController which allow you to create a new SlapChat.      

### Hints


##Location 

### Extra Credit
Your TableViewController displaying all of your current pictures is actually better suited as a UICollectionViewController.  Collection Views are implemented nearly identically to Table Views.  Figure out how to implement a Collection View Controller.  Use the Documentation!  

### Links 


