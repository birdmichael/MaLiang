# ![](Images/icon-32.png) MaLiang

[![CI Status](http://img.shields.io/travis/Harley-xk/MaLiang.svg?style=flat)](https://travis-ci.org/Harley-xk/MaLiang)
[![Version](https://img.shields.io/cocoapods/v/MaLiang.svg?style=flat)](http://cocoapods.org/pods/MaLiang)
[![Language](https://img.shields.io/badge/language-Swift%204-orange.svg)](https://swift.org)
[![codebeat badge](https://codebeat.co/badges/438159fd-b5f9-43d4-a1d5-b07ba5e6cf03)](https://codebeat.co/projects/github-com-harley-xk-maliang-metal)
[![License](https://img.shields.io/cocoapods/l/MaLiang.svg?style=flat)](http://cocoapods.org/pods/MaLiang)
[![Platform](https://img.shields.io/cocoapods/p/MaLiang.svg?style=flat)](http://cocoapods.org/pods/MaLiang)

🎉 MaLiang is on Metal now!

MaLiang is a painting framework based on Metal. The name of "MaLiang" comes from a boy who had a magical brush in Chinese ancient fairy story.

[Simplified Chinese](https://www.jianshu.com/p/13849a90064a)

<img src="Images/sample.jpg" width=400></img>

## Requirements

iOS 9.0+, Swift 4.2+ </br>

The core painting module is based on Metal</br>

You can simply make it compatible with lower version of iOS and swift by changing only serval lines of code.

## Installation

MaLiang is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
# 2.0.0 is currently in beta testing
pod 'MaLiang', '~> 2.0.0-beta-2'
```

To use the old OpenGL ES verion:

```ruby
pod 'MaLiang', '~> 1.1'
```

## Usage

MaLiang is simple to use.

1. import MaLiang
2. enjoy painting!

### Canvas

```swift
open class Canvas: MetalView
```

A `Canvas` is the basic component of `MaLiang`. You will paint all things on it.
`Canvas` extends from `MetalView`, whitch extends from `MTKView`. `MetalView` handles all the logic with MetalKit and hides them from you.

`Canvas` can be simply created with xib or code.

- with xib or storyboard, simply drag and drop an `UIView` object into your view controller and change it's class to `Canvas` and module to `MaLiang`
- with code, just create with `init(frame:)` as any `UIView` you do before.

Now, all things necessary is done!

#### Snapshot

You can take snapshot on canvas now. Just call `snapshot` function on `Canvas` and you will get an optional `UIImage` object.

### Brush

With all things done, you can do more with `Brush`!

`Brush` is the key feature to `MaLiang`. It holds textures and colors, whitch makes it possiable to paint amazing things.

Register a `Brush` with image data or file to Canvas and paint with it:

```swift
let path = Bundle.main.path(forResource: "pencil", ofType: "png")!
let pencil = try? canvas.registerBrush(with: URL(fileURLWithPath: path))
pencil?.use()
```

`Brush` have serval properties for you to custmize:

```swift
// opacity of texture, affects the darkness of stroke
// set opacity to 1 may cause heavy aliasing
open var opacity: CGFloat = 0.3

// width of stroke line in points
open var pointSize: CGFloat = 4

// this property defines the minimum distance (measureed in points) of nearest two textures
// defaults to 1, this means erery texture calculated will be rendered, dictance calculation will be skiped
open var pointStep: CGFloat = 1

// sensitive of pointsize changed from force, from 0 - 1
open var forceSensitive: CGFloat = 0

/// color of stroke
open var color: UIColor = .black
```

With all these properties, you can create you own brush as your imagination.

#### Force & 3D Touch

MaLiang supports automatically adjustment of stroke size with painting force. 3D Touch is supported by default, and simulated force will be setup on devices those are not supporting this.

`forceSensitive` is the property that force affects the storke size. It should be set between `0` to `1`. the smaller the value is, the less sensitive will be. if sets to `0`, then force will not affects the stroke size.

### Document

`Document` is now configured by default. It holds all the data on the `Canvas`, and makes the **undo** and **redo** actions to be possiable. </br>
And you can implement your own **saving logic** with the data holds by `Document`.

## TODO

- [x] Port to Metal
- [x] Undo & Redo
- [x] Export to image
- [x] Optimize for scale
- [ ] Optimize for saving logic
- [ ] Glow style line
- [ ] Text element
- [ ] Image element
- [ ] Texture rotation

## License

MaLiang is available under the MIT license. See the LICENSE file for more info.
