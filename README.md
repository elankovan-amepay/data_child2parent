## How to pass data from child to parent widget in flutter ?

```dart
import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {

  int numberForChanging = 0;

  void refresh(int getNumber){
    setState(() {
      numberForChanging = getNumber;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Home Page"),
      ),
      body: Column(
        children: [
          Container(
            color: Colors.blue.shade100,
              height: 100.0,
              width: double.infinity,
              child: Column(
                children: [
                  Text("${numberForChanging}"),
                  Text("parent-widget"),
                ],
              )),
          ChildWidget(
            numberForChanging: numberForChanging,
            getfunc: refresh,
          ),
        ],
      ),
    );
  }
}

class ChildWidget extends StatelessWidget {
  ChildWidget({Key? key, this.numberForChanging, this.getfunc}) : super(key: key);

  final dynamic getfunc;
  int? numberForChanging;

  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.amber.shade100,
      width: double.infinity,
      height: 100.0,
      child: Column(
        children: [
          Text("child-widget"),
          ElevatedButton(
            child: Text("click"),
            onPressed: (){
              numberForChanging = numberForChanging! + 1;
              getfunc(numberForChanging);
            },
          ),
        ],
      ),
    );
  }
}
```
