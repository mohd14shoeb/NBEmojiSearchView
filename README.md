NBEmojiSearchView
====================
This view makes it easy to integrate a searchable emoji dropdown into your iOS app in just a few lines.

![](screencast.gif)

##Installation
###CocoaPods
[CocoaPods](http://cocoapods.org) is a dependency manager for Objective-C, which automates and simplifies the process of using 3rd-party libraries like NBSlideUpView in your projects.

```ruby
pod "NBEmojiSearchView"
```

###Alternative
Alternatively, you can just drag the <b>Source</b> folder into your project.

##Usage
Instantiate an `NBEmojiSearchView`, then install it on a `UITextField` as shown below. 
```smalltalk
NBEmojiSearchView *emojiSearchView = [[NBEmojiSearchView alloc] init];
[emojiSearchView installOnTextField:textField];
```
You control sizing and placement of the `searchView`. The `searchView` will appear and disappear at the appropriate times automatically.

###Customization

The `UITableView` that displays results is exposed.
```smalltalk
@property (nonatomic, strong) UITableView *tableView;
```

#### Animation

The appearance and disappearance animations. Set these blocks with custom animations you'd like the `searchView` to execute.

If you choose to customize these the appear or disappear animation, you MUST call `appearAnimationDidFinish` or `disappearAnimationDidFinish` when the animation completes, respectively.
```smalltalk
@property (nonatomic, copy) void (^appearAnimationBlock)(); "Default: A non-animated alpha change from 0.0 to 1.0."
@property (nonatomic, copy) void (^disappearAnimationBlock)(); "Default: A non-animated alpha change from 1.0 to 0.0."
```

**Example**

```smalltalk
self.emojiSearchView.appearAnimationBlock = ^{
    [UIView animateWithDuration:0.2 animations:^{
        weakSelf.emojiSearchView.alpha = 1.0;
    } completion:^(BOOL finished) {
        [weakSelf.emojiSearchView appearAnimationDidFinish];
    }];
};
```

#### Other Visuals

The font of the emoji result cells.
```smalltalk
@property (nonatomic, strong) UIFont *font;
```

The text color of the emoji result cells.
```smalltalk
@property (nonatomic, strong) UIColor *textColor;
```

The header title of the `tableView` that displays emoji search results.
```smalltalk
@property (nonatomic, strong) NSString *headerTitle;
```

###Delegate Methods

These delegate methods revolve around the appearance and disappearance of the search view. Please [let me know](http://twitter.com/2neeraj) or PR if you'd like additional delegate methods.
```smalltalk
- (void)emojiSearchViewWillAppear:(NBEmojiSearchView *)emojiSearchView;
- (void)emojiSearchViewDidAppear:(NBEmojiSearchView *)emojiSearchView;
- (void)emojiSearchViewWillDisappear:(NBEmojiSearchView *)emojiSearchView;
- (void)emojiSearchViewDidDisappear:(NBEmojiSearchView *)emojiSearchView;
```

