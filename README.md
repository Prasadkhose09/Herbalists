# Herbalists
import 'package:flutter/material.dart';
import 'dart:async'; // For Timer
import 'package:model_viewer_plus/model_viewer_plus.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Virtual Herbal Garden',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.green),
        useMaterial3: true,
      ),
      home: const SplashScreen(), // Set the splash screen as the initial page
    );
  }
}

// Splash Screen
class SplashScreen extends StatefulWidget {
  const SplashScreen({super.key});

  @override
  _SplashScreenState createState() => _SplashScreenState();
}

class _SplashScreenState extends State<SplashScreen> {
  @override
  void initState() {
    super.initState();

    // Navigate to the login screen after 3 seconds
    Timer(const Duration(seconds: 3), () {
      Navigator.pushReplacement(
        context,
        MaterialPageRoute(builder: (context) => const LoginScreen()),
      );
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        decoration: const BoxDecoration(
          image: DecorationImage(
            image: AssetImage("assets/images/splash2.jpg"), // Splash screen image
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}

// Login Screen with background image and opacity
class LoginScreen extends StatelessWidget {
  const LoginScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          // Background Image with opacity
          Container(
            decoration: BoxDecoration(
              image: DecorationImage(
                image: AssetImage('assets/images/Backg.jpg'),
                fit: BoxFit.cover,
                colorFilter: ColorFilter.mode(
                  Colors.black.withOpacity(0.4), // Adjust opacity here
                  BlendMode.darken,
                ),
              ),
            ),
          ),
          // Login Form
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  const Text(
                    'Login to Virtual Herbal Garden',
                    style: TextStyle(
                      fontSize: 22,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                    ),
                  ),
                  const SizedBox(height: 30,),
                  const SizedBox(height: 40),
                  TextField(
                    decoration: InputDecoration(
                      labelText: "Email",
                      prefixIcon: const Icon(Icons.email, color: Colors.white),
                      labelStyle: const TextStyle(color: Colors.white),
                      filled: true,
                      fillColor: Colors.white.withOpacity(0.3),
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(10.0),
                      ),
                    ),
                  ),

                  const SizedBox(height: 30),
                  TextField(
                    obscureText: true,
                    decoration: InputDecoration(
                      labelText: "Password",
                      prefixIcon: const Icon(Icons.lock, color: Colors.white),
                      labelStyle: const TextStyle(color: Colors.white),
                      filled: true,
                      fillColor: Colors.white.withOpacity(0.3),
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(10.0),
                      ),
                    ),
                  ),
                  const SizedBox(height: 20,),
                  const SizedBox(height: 30),
                  ElevatedButton(
                    onPressed: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) =>
                          const MyHomePage(title: 'We are Team Herbalist!'),
                        ),
                      );
                    },

                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.green,
                      padding: const EdgeInsets.symmetric(horizontal: 50, vertical: 15),
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(10.0),
                      ),
                    ),
                    child: const Text(
                      'Login',
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }
}

// Main Home Page (Herbs display)
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: SingleChildScrollView(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Stack(
              alignment: Alignment.center,
              children: [
                Container(
                  width: double.infinity,
                  height: 120,
                  decoration: BoxDecoration(
                    image: DecorationImage(
                      image: AssetImage('assets/images/garden.jpg'),
                      fit: BoxFit.cover,
                      colorFilter: ColorFilter.mode(
                        Colors.black.withOpacity(0.5),
                        BlendMode.darken,
                      ),
                    ),
                  ),
                ),
                const Text(
                  'Welcome to Virtual Herbal Garden',
                  style: TextStyle(
                    fontSize: 23,
                    color: Colors.white,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ],
            ),
            const SizedBox(height: 20),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                _buildHerbCard(
                  context,
                  title: 'Coriander',
                  imagePath: 'assets/images/images.jpg',
                  onTap: () {
                    print("Clicked on Dhaniya");
                  },
                ),
                const SizedBox(width: 10),
                _buildHerbCard(
                  context,
                  title: 'Turmeric (Haldi)',
                  imagePath: 'assets/images/download.webp',
                  onTap: () {
                    print("Clicked on Haldi");
                  },
                  onDoubleTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (context) => ModelViewerScreen(),
                      ),
                    );
                  },
                ),
              ],
            ),
            const SizedBox(height: 20),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                _buildHerbCard(
                  context,
                  title: 'Ashwagandha',
                  imagePath: 'assets/images/download.jpg',
                  onTap: () {
                    print("Clicked on Ashwagandha");
                  },
                ),
                const SizedBox(width: 10),
                _buildHerbCard(
                  context,
                  title: 'Neem',
                  imagePath: 'assets/images/Neem.jpg',
                  onTap: () {
                    print("Clicked on Neem");
                  },
                ),
              ],
            ),
            const SizedBox(height: 20),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                _buildHerbCard(
                  context,
                  title: 'Amla',
                  imagePath: 'assets/images/Amla.jpg',
                  onTap: () {
                    print("Clicked on Amla");
                  },
                ),
                const SizedBox(width: 10),
                _buildHerbCard(
                  context,
                  title: 'Tulsi',
                  imagePath: 'assets/images/Tulsi.jpg',
                  onTap: () {
                    print("Clicked on Tulsi");
                  },
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildHerbCard(
      BuildContext context, {
        required String title,
        required String imagePath,
        VoidCallback? onTap,
        VoidCallback? onDoubleTap,
      }) {
    return InkWell(
      onTap: onTap,
      onDoubleTap: onDoubleTap,
      child: Container(
        width: 150,
        child: Column(
          children: [
            Container(
              width: 150,
              height: 150,
              child: Image.asset(
                imagePath,
                fit: BoxFit.cover,
              ),
            ),
            const SizedBox(height: 10),
            Text(
              title,
              style: const TextStyle(fontSize: 18),
              textAlign: TextAlign.center,
            ),
          ],
        ),
      ),
    );
  }
}

class ModelViewerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("3D View: Haldi"),
      ),
      body: Center(
        child: ModelViewer(
          src: 'assets/haldi.glb', // Path to the 3D model
          alt: "A 3D model of Haldi",
          ar: true, // Enable AR view
          autoRotate: true, // Enable auto-rotation
          cameraControls: true, // Enable camera controls

        ),

      ),

    );

  }
}


