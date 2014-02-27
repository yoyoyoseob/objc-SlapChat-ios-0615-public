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

###Project Overview 

The goal behind this lab is to build the next Billion dollar App, SlapChat.  SlapChat turns the idea of anonymous photo-sending on its head by allowing you to save and share your precious photos. If anyone is interested in investing, we are accepting investments with a minimum of $100 million. 

#### Specifics

Upon launch, you'll land on a UITableView Controller.  The table view will load in an array of saved pictures from Core Data. Tapping on a cell will open a UIActivityViewController which will allow you to share your photo VIA text, or Email.  The navigation bar will have a + button which will open up a new `UIImagePickerController` that allows you to grab a photo. When someone selects a photo they are then brought back to the `UITableView` with the creation date and time (formatted "MM/dd/yyyy HH:mm").

### Instructions

  1. Make a new Project with a `UITableViewController` and a plus button for the right `UIBarButtonItem`
  2. Create a new class `FISMessage` that has two properties: date and image.
  3. Create a dataStore singelton. Add an `NSArray` property that will hold your `FISMessage` objects
  4. When the add button is tapped, a `UIImagePickerController` is brought up and the user selects an image
  5. When the image is selected a new `FISMessage` should be added to the `UITableView` with the new message.
  6. Ok so kill the app... Double tap on the home button and swipe the app up to kill the app.  
  7. Relaunch the app.  All of your photos are gone, and this sucks. Let's fix this by implementing persistance via coredata.  

### Core Data Instructions 

  1. First, create your Data Model by selecting `new file -> Core Data -> Data Model` 
  2. Name your object Model and save. 
  3. Open your `Model.xcdatamodeld` file.  This is where you'll configure your entity.  
  4. Add a new entity and call it `FISMessage`
  5. Add two attributes for FISMessage: date and image.  date will be of type Date and image will be of type binary data. 

## Core Data Stack 

Next we'll build the core data stack to allow us to communicate with Core Data.  

Your DataStore.h should look like this. 

```objc 
@interface DataStore : NSObject

@property (strong,nonatomic) NSManagedObjectContext *managedObjectContext;
@property (strong,nonatomic) NSPersistentStoreCoordinator *persistentStoreCoordinator;
@property (strong,nonatomic) NSManagedObjectModel *managedObjectModel;

+ (DataStore *) sharedStore;

```

First let's implement our managedObject model property.  We'll use the managedObjectModel's getter method to set the managed object model lazily (the first time it's called).  Here is what the getter will look like.  Make you sure you get a handle on what this code is doing.  

```objc 
- (NSManagedObjectModel *)managedObjectModel
{
    if (!_managedObjectModel) //in other words, if managedObjectModel == nil
    {
        NSURL *modelURL = [[NSBundle mainBundle] URLForResource:@"Model" withExtension:@"momd"]; 
        _managedObjectModel = [[NSManagedObjectModel alloc] initWithContentsOfURL:modelURL];
    }
    return _managedObjectModel;
}
```

Now that we've got an `NSManagedObjectModel` let's move on to the `NSPersistentStoreCoordinator`. 

```objc

- (NSPersistentStoreCoordinator *)persistentStoreCoordinator
{
    if (!_persistentStoreCoordinator)
    {
        NSURL *storeURL = [[self applicationDocumentsDirectory] URLByAppendingPathComponent:@"Model.sqlite"];
        NSError *error = nil;
        _persistentStoreCoordinator = [[NSPersistentStoreCoordinator alloc] initWithManagedObjectModel:[self managedObjectModel]];
        if (![_persistentStoreCoordinator addPersistentStoreWithType:NSSQLiteStoreType configuration:nil URL:storeURL options:nil error:&error]) {
            NSLog(@"Unresolved error %@, %@", error, [error userInfo]);
            abort();
        }
    }
    return _persistentStoreCoordinator;
}
```
Our `NSPersistentStoreCoordinator` references a method we haven't implemented yet.  Let's implement the `applicationDocumentsDirectory` method 

```objc
// Returns the URL to the application's Documents directory.
- (NSURL *)applicationDocumentsDirectory
{
    return [[[NSFileManager defaultManager] URLsForDirectory:NSDocumentDirectory inDomains:NSUserDomainMask] lastObject];
}
```

Next let's configure our `managedObjectContext` getter method.

```objc
- (NSManagedObjectContext *)managedObjectContext
{
    if (!_managedObjectContext)
    {
        NSPersistentStoreCoordinator *coordinator = self.persistentStoreCoordinator;
        if (coordinator)
        {
            _managedObjectContext = [[NSManagedObjectContext alloc] init];
            [_managedObjectContext setPersistentStoreCoordinator:coordinator];
        }
    }
    return _managedObjectContext;
}
```

Let's think about what this code does for a second.  The main property you'll be externally accessing in your CoreData stack is the NSManagedObjectContext.  The first time you access your managed object context, the NSManagedObjectContext calls `- (NSPersistentStoreCoordinator *)persistentStoreCoordinator //getter method`.  Since the persistentStoreCoordinator doesn't yet exist, it is created and saved.  The persistentStoreCoordinator object calls the managedObjectModel, which also creates itself.  
This chain reaction builds your core data stack upon the first call to your managedObjectModel.  


## Saving and Fetching 

- Your TableView should fetch an array of FISMessage objects and load that array into the table.  
-  The + UIBarButtonItem in the table view's navigation bar should link to an action that calls a UIImagePicker, which gets a photo 

### Hints


##Location 

### Links 


