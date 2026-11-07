# DaySpark
Group Project
import 'dart:math';
  import 'package:flutter/material.dart';

  void main() {
    runApp(const DoMoreApp());
  }

  class DoMoreApp extends StatelessWidget {
  const DoMoreApp({super.key});

  @override
  Widget build(BuildContext context) {
  return MaterialApp(
  title: 'DoMore',
  debugShowCheckedModeBanner: false,
  theme: ThemeData(
  colorScheme: ColorScheme.fromSeed(
  seedColor: Colors.blue,
  ),
  useMaterial3: true,
  ),
  home: const HomeScreen(),
  );
  }
  }

// ---------------- HOME SCREEN ----------------

  class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
  return Scaffold(
  appBar: AppBar(
  title: const Text('DoMore 🎯'),
  centerTitle: true,
  ),
  body: Center(
  child: Padding(
  padding: const EdgeInsets.all(24),
  child: Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
  const Icon(
  Icons.explore,
  size: 100,
  color: Colors.blue,
  ),

  const SizedBox(height: 20),

  const Text(
  'Stop Scrolling.\nStart Doing.',
  textAlign: TextAlign.center,
  style: TextStyle(
  fontSize: 30,
  fontWeight: FontWeight.bold,
  ),
  ),

  const SizedBox(height: 15),

  const Text(
  'Find something fun or productive to do right now!',
  textAlign: TextAlign.center,
  style: TextStyle(fontSize: 16),
  ),

  const SizedBox(height: 40),

  ElevatedButton(
  onPressed: () {
  Navigator.push(
  context,
  MaterialPageRoute(
  builder: (context) => const PreferencesScreen(),
  ),
  );
  },
  child: const Text('Find an Activity'),
  ),

  const SizedBox(height: 15),

  ElevatedButton.icon(
  icon: const Icon(Icons.casino),
  label: const Text('Surprise Me!'),
  onPressed: () {
  Navigator.push(
  context,
  MaterialPageRoute(
  builder: (context) => const SurpriseScreen(),
  ),
  );
  },
  ),
  ],
  ),
  ),
  ),
  );
  }
  }

// ---------------- PREFERENCES SCREEN ----------------

  class PreferencesScreen extends StatefulWidget {
  const PreferencesScreen({super.key});

  @override
  State<PreferencesScreen> createState() => _PreferencesScreenState();
  }

  class _PreferencesScreenState extends State<PreferencesScreen> {
  String selectedMood = 'Bored';
  String selectedTime = '15–30 min';
  String selectedBudget = 'Free';
  String selectedLocation = 'Indoors';

  @override
  Widget build(BuildContext context) {
  return Scaffold(
  appBar: AppBar(title: const Text('Your Preferences')),
  body: SingleChildScrollView(
  padding: const EdgeInsets.all(20),
  child: Column(
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
  const Text(
  'How are you feeling?',
  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
  ),

  DropdownButton<String>(
  value: selectedMood,
  isExpanded: true,
  items: ['Happy', 'Tired', 'Bored', 'Stressed', 'Energetic']
      .map((mood) {
  return DropdownMenuItem(
  value: mood,
  child: Text(mood),
  );
  }).toList(),
  onChanged: (value) {
  setState(() {
  selectedMood = value!;
  });
  },
  ),

  const SizedBox(height: 25),

  const Text(
  'How much time do you have?',
  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
  ),

  DropdownButton<String>(
  value: selectedTime,
  isExpanded: true,
  items: ['5–15 min', '15–30 min', '30–60 min', '1+ hour']
      .map((time) {
  return DropdownMenuItem(
  value: time,
  child: Text(time),
  );
  }).toList(),
  onChanged: (value) {
  setState(() {
  selectedTime = value!;
  });
  },
  ),

  const SizedBox(height: 25),

  const Text(
  'What is your budget?',
  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
  ),

  DropdownButton<String>(
  value: selectedBudget,
  isExpanded: true,
  items: ['Free', 'Low Cost', 'Any']
      .map((budget) {
  return DropdownMenuItem(
  value: budget,
  child: Text(budget),
  );
  }).toList(),
  onChanged: (value) {
  setState(() {
  selectedBudget = value!;
  });
  },
  ),

  const SizedBox(height: 25),

  const Text(
  'Where do you want to be?',
  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
  ),

  DropdownButton<String>(
  value: selectedLocation,
  isExpanded: true,
  items: ['Indoors', 'Outdoors'].map((location) {
  return DropdownMenuItem(
  value: location,
  child: Text(location),
  );
  }).toList(),
  onChanged: (value) {
  setState(() {
  selectedLocation = value!;
  });
  },
  ),

  const SizedBox(height: 40),

  Center(
  child: ElevatedButton(
  child: const Text('Find Activities'),
  onPressed: () {
  Navigator.push(
  context,
  MaterialPageRoute(
  builder: (context) => ActivityScreen(
  mood: selectedMood,
  time: selectedTime,
  budget: selectedBudget,
  location: selectedLocation,
  ),
  ),
  );
  },
  ),
  ),
  ],
  ),
  ),
  );
  }
  }

// ---------------- ACTIVITY SCREEN ----------------

  class ActivityScreen extends StatelessWidget {
  final String mood;
  final String time;
  final String budget;
  final String location;

  const ActivityScreen({
  super.key,
  required this.mood,
  required this.time,
  required this.budget,
  required this.location,
  });

  List<String> getActivities() {
  if (location == 'Outdoors') {
  return [
  '🚶 Go for a walk',
  '🌳 Visit a park',
  '📸 Take pictures outside',
  ];
  }

  if (mood == 'Tired') {
  return [
  '📖 Read a book',
  '🎵 Listen to relaxing music',
  '🧘 Try a short meditation',
  ];
  }

  return [
  '🎨 Draw something',
  '🧁 Try baking',
  '🎮 Play a game',
  '📚 Learn a new skill',
  ];
  }

  @override
  Widget build(BuildContext context) {
  final activities = getActivities();

  return Scaffold(
  appBar: AppBar(title: const Text('Activities for You')),
  body: Padding(
  padding: const EdgeInsets.all(20),
  child: Column(
  children: [
  Text(
  'Based on your mood: $mood',
  style: const TextStyle(fontSize: 18),
  ),

  const SizedBox(height: 20),

  Expanded(
  child: ListView.builder(
  itemCount: activities.length,
  itemBuilder: (context, index) {
  return Card(
  child: ListTile(
  title: Text(
  activities[index],
  style: const TextStyle(fontSize: 18),
  ),
  subtitle: Text('$time • $budget • $location'),
  trailing: const Icon(Icons.arrow_forward),
  ),
  );
  },
  ),
  ),

  ElevatedButton.icon(
  icon: const Icon(Icons.casino),
  label: const Text('Surprise Me!'),
  onPressed: () {
  Navigator.push(
  context,
  MaterialPageRoute(
  builder: (context) => const SurpriseScreen(),
  ),
  );
  },
  ),
  ],
  ),
  ),
  );
  }
  }

// ---------------- SURPRISE ME SCREEN ----------------

  class SurpriseScreen extends StatefulWidget {
  const SurpriseScreen({super.key});

  @override
  State<SurpriseScreen> createState() => _SurpriseScreenState();
  }

  class _SurpriseScreenState extends State<SurpriseScreen> {
  final List<String> challenges = [
  '🎨 Draw something for 10 minutes!',
  '🚶 Take a 15-minute walk!',
  '📚 Learn something new for 20 minutes!',
  '🧹 Clean one small area of your room!',
  '🎵 Listen to your favorite song without scrolling!',
  ];

  String challenge = 'Tap the button to get a challenge!';

  void getChallenge() {
  final random = Random();

  setState(() {
  challenge = challenges[random.nextInt(challenges.length)];
  });
  }

  @override
  Widget build(BuildContext context) {
  return Scaffold(
  appBar: AppBar(title: const Text('Surprise Me! 🎲')),
  body: Center(
  child: Padding(
  padding: const EdgeInsets.all(30),
  child: Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
  const Text(
  'STOP SCROLLING, START DOING!',
  textAlign: TextAlign.center,
  style: TextStyle(
  fontSize: 22,
  fontWeight: FontWeight.bold,
  ),
  ),

  const SizedBox(height: 40),

  Text(
  challenge,
  textAlign: TextAlign.center,
  style: const TextStyle(fontSize: 24),
  ),

  const SizedBox(height: 40),

  ElevatedButton(
  onPressed: getChallenge,
  child: const Text('Give Me a Challenge!'),
  ),
  ],
  ),
  ),
  ),
  );
  }
  }
