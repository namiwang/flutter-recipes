# flutter-recipes

just some snippets with flutter

## image with loader

```dart
class ImageWithLoader extends StatefulWidget {
  final String imgSrc;

  ImageWithLoader(@required this.imgSrc, { Key key }) : super(key: key);

  @override
  _ImageWithLoaderState createState() => new _ImageWithLoaderState();
}

class _ImageWithLoaderState extends State<ImageWithLoader> {
  Image image;

  @override
  void initState() {
    super.initState();

    _fetchImg();
  }

  @override
  Widget build(BuildContext context) {
    if ( image == null ) {
      return new Container(
        child: const CircularProgressIndicator(),
        alignment: FractionalOffset.center,
      );
    } else {
      return image;
    }
  }

  Future<Null> _fetchImg() async {
    final Uint8List bytes = await http.readBytes(widget.imgSrc);
    setState((){ image = new Image.memory(bytes);});
  }
}
```

NOTE: 

1. `FutureBuilder` should be better for this purpose, though it leads to some weird flickers.
2. seems that images created with `.memory` wont be cached automatically. needs refinements with that.

## text as link

```dart
class _LinkTextSpan extends TextSpan {
  _LinkTextSpan({ TextStyle style, String url, String text }) : super(
    style: style,
    text: text ?? url,
    recognizer: new TapGestureRecognizer()..onTap = () {
      urlLauncher.launch(url);
    }
  );
}
```

NOTE:

- ripped from Gallery

## global key

TBD

## image caching

TBD
