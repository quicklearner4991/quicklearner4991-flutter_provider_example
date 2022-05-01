# What is provider?

A wrapper around InheritedWidget to make them easier to use and more reusable.

By using provider instead of manually writing InheritedWidget, you get:

a) Simplified allocation/disposal of resources

b) Lazy-loading

c) A vastly reduced boilerplate over making a new class every time

d) Devtool friendly – using Provider, the state of your application will be visible in the Flutter devtool

e) A common way to consume these InheritedWidgets
increased scalability for classes with a listening mechanism that grows exponentially in complexity (such as ChangeNotifier, which is O(N) for dispatching notifications).


# STEP 1 : Add this in pubspec file in dependency section to add provider library to your project
```
provider: ^6.0.2
```

# Step 2 : Add your providers class in main home class like this
```
@override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => SignupProvider()),
      ],
      child: MaterialApp(...)
      
      );
      
      }
 ```
      
      
# Step 3 : Create provider class and code as per your requirement , extend the class with ChangeNotifier

```
import 'package:flutter/material.dart';

class SignupProvider extends ChangeNotifier {
  var _count = 10;
  int get getCounter {
    return _count;
  }

  void incrementCounter() {
    _count += 1;
    notifyListeners();
  }
}
```

# Step 4 - Using a basic example to increment counter , Core logic is implemented in provider class

```
import 'package:cs_flutter/providers/signup_provider.dart';
import 'package:cs_flutter/utils/common/CsDimens.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class SignupScreen extends StatefulWidget {
  const SignupScreen( this.title, {Key? key}) : super(key: key);
  final int title;
  @override
  _SignupScreenState createState() => _SignupScreenState();
}

class _SignupScreenState extends State<SignupScreen> {
  @override
  void initState() {
    super.initState();
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        alignment: Alignment.center,
        child: InkWell(
          onTap: () {
            context.read<SignupProvider>().incrementCounter();
          },
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: [
              SizedBox(height: 100.0,),
              Text('Press to increment',style: TextStyle(fontSize: CsDimens.SPACE28),),
              Text(context.watch<SignupProvider>().getCounter.toString(),style: TextStyle(fontSize: CsDimens.SPACE28),)
            ],
          ),
        ),
      ),
    );
  }
}
  ```
