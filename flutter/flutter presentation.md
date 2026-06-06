StatefulWidget => interface/props

State => actual implementation

```dart
import 'package:flutter/material.dart';

// 1. THE INTERFACE (Immutable Blueprint)
// Like React Props: { onScan: (code: string) => void, overlayColor?: string }
class QRScannerWidget extends StatefulWidget {
  final Function(String code) onScan; // Output (Callback)
  final Color overlayColor;           // Input (Style)

  const QRScannerWidget({
    super.key, 
    required this.onScan, 
    this.overlayColor = Colors.black54,
  });

  @override
  State<QRScannerWidget> createState() => _QRScannerWidgetState();
}

// 2. THE CONTAINER (Mutable Logic & UI)
class _QRScannerWidgetState extends State<QRScannerWidget> {
  // INTERNAL STATE: Not visible to the outside
  bool _isCameraInitialized = false;
  late String _currentStatus; 

  @override
  void initState() {
    super.initState();
    // Similar to useEffect(() => { init() }, [])
    _currentStatus = "Waiting for camera...";
    _initializeCamera();
  }

  void _initializeCamera() async {
    // Logic for camera...
    setState(() => _isCameraInitialized = true);
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      color: widget.overlayColor, // Accessing "Props" via 'widget.'
      child: Column(
        children: [
          Text(_currentStatus), // Accessing "Internal State"
          if (_isCameraInitialized) 
            ElevatedButton(
              onPressed: () {
                // Emitting the event back to the Parent
                widget.onScan("MOCK_QR_CODE_123"); 
              },
              child: const Text("Simulate Scan"),
            ),
        ],
      ),
    );
  }

  @override
  void dispose() {
    // Like useEffect cleanup: return () => { camera.stop() }
    super.dispose();
  }
}
```