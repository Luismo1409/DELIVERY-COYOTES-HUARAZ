# DELIVERY-COYOTES-HUARAZ
import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

void main() {
  runApp(VoyDeliveryApp());
}

class VoyDeliveryApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Voy Delivery',
      theme: ThemeData(
        primaryColor: Colors.amber[700],
        scaffoldBackgroundColor: Colors.grey[100],
      ),
      home: HomeScreen(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class HomeScreen extends StatelessWidget {
  final String phoneNumber = '51900147248'; // 51 = Perú

  void _sendWhatsApp(String message) async {
    final url = 'https://wa.me/$phoneNumber?text=${Uri.encodeComponent(message)}';
    if (await canLaunchUrl(Uri.parse(url))) {
      await launchUrl(Uri.parse(url), mode: LaunchMode.externalApplication);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Voy Delivery Huaraz'),
        backgroundColor: Colors.amber[700],
      ),
      body: SingleChildScrollView(
        child: Column(
          children: [
            // Logo con coyote
            Container(
              color: Colors.amber[700],
              padding: EdgeInsets.all(20),
              width: double.infinity,
              child: Column(
                children: [
                  CircleAvatar(
                    radius: 60,
                    backgroundColor: Colors.white,
                    child: Icon(Icons.motorcycle, size: 50, color: Colors.amber[700]),
                  ),
                  SizedBox(height: 10),
                  Text('VOY', style: TextStyle(fontSize: 32, fontWeight: FontWeight.bold, color: Colors.white)),
                  Text('DELIVERY ENVIOS EN TODO HUARAZ', style: TextStyle(color: Colors.white70)),
                ],
              ),
            ),

            SizedBox(height: 20),

            // Botones de acción
            Padding(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                children: [
                  _buildButton(context, '📋 Ver Menú', 'MENÚ'),
                  _buildButton(context, '🛵 Hacer Pedido', 'Hola, quiero hacer un pedido'),
                  _buildButton(context, '📍 Enviar Ubicación', 'UBICACIÓN'),
                  _buildButton(context, '💰 Consultar Precio', 'PRECIO'),
                  _buildButton(context, '📞 Hablar con Agente', 'AGENTE'),
                ],
              ),
            ),

            SizedBox(height: 30),

            // Info de contacto
            Card(
              margin: EdgeInsets.all(20),
              child: Padding(
                padding: EdgeInsets.all(15),
                child: Column(
                  children: [
                    Text('Contacto Directo', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
                    SizedBox(height: 10),
                    Text('📱 900147248'),
                    Text('📍 Huaraz, Áncash'),
                    Text('⏰ Lun-Dom 9am - 10pm'),
                  ],
                ),
              ),
            )
          ],
        ),
      ),
    );
  }

  Widget _buildButton(BuildContext context, String text, String message) {
    return Padding(
      padding: EdgeInsets.only(bottom: 15),
      child: ElevatedButton(
        style: ElevatedButton.styleFrom(
          backgroundColor: Colors.amber[700],
          minimumSize: Size(double.infinity, 50),
          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
        ),
        onPressed: () => _sendWhatsApp(message),
        child: Text(text, style: TextStyle(fontSize: 16, color: Colors.white)),
      ),
    );
  }
}
