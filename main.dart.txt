import 'package:flutter/material.dart';

void main() {
  runApp(GestaoAbrigosApp());
}

class GestaoAbrigosApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gestão de Abrigos',
      home: AbrigosPage(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class Abrigo {
  final String nome;
  final String endereco;
  final int capacidadeMaxima;
  int capacidadeAtual;

  Abrigo({
    required this.nome,
    required this.endereco,
    required this.capacidadeMaxima,
    required this.capacidadeAtual,
  });

  bool get estaLotado => capacidadeAtual >= capacidadeMaxima;
}

class AbrigosPage extends StatefulWidget {
  @override
  _AbrigosPageState createState() => _AbrigosPageState();
}

class _AbrigosPageState extends State<AbrigosPage> {
  List<Abrigo> abrigos = [
    Abrigo(nome: 'Ginásio Municipal', endereco: 'Rua das Flores, 123 - Centro', capacidadeMaxima: 100, capacidadeAtual: 60),
    Abrigo(nome: 'Escola Central', endereco: 'Av. Brasil, 456 - Bairro Alto', capacidadeMaxima: 80, capacidadeAtual: 75),
    Abrigo(nome: 'Igreja São José', endereco: 'Rua da Paz, 789 - Vila Nova', capacidadeMaxima: 50, capacidadeAtual: 45),
    Abrigo(nome: 'Centro Comunitário', endereco: 'Travessa do Sol, 234 - Bairro Feliz', capacidadeMaxima: 70, capacidadeAtual: 70),
    Abrigo(nome: 'Clube do Povo', endereco: 'Av. Esperança, 321 - Bairro Luz', capacidadeMaxima: 60, capacidadeAtual: 30),
    Abrigo(nome: 'Ginásio do Bairro Verde', endereco: 'Rua Verdejante, 99 - Bairro Verde', capacidadeMaxima: 90, capacidadeAtual: 90),
  ];

  void _incrementarCapacidade(int index) {
    setState(() {
      if (abrigos[index].capacidadeAtual < abrigos[index].capacidadeMaxima) {
        abrigos[index].capacidadeAtual++;
      }
    });
  }

  void _decrementarCapacidade(int index) {
    setState(() {
      if (abrigos[index].capacidadeAtual > 0) {
        abrigos[index].capacidadeAtual--;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gestão de Abrigos'),
      ),
      body: ListView.builder(
        itemCount: abrigos.length,
        itemBuilder: (context, index) {
          final abrigo = abrigos[index];
          return Card(
            margin: EdgeInsets.all(10),
            child: Padding(
              padding: EdgeInsets.all(12),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    abrigo.nome,
                    style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                  ),
                  SizedBox(height: 4),
                  Text(abrigo.endereco),
                  SizedBox(height: 4),
                  Text('Capacidade Máxima: ${abrigo.capacidadeMaxima}'),
                  Text('Capacidade Atual: ${abrigo.capacidadeAtual}'),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Row(
                        children: [
                          IconButton(
                            icon: Icon(Icons.remove_circle),
                            onPressed: () => _decrementarCapacidade(index),
                          ),
                          IconButton(
                            icon: Icon(Icons.add_circle),
                            onPressed: () => _incrementarCapacidade(index),
                          ),
                        ],
                      ),
                      Icon(
                        abrigo.estaLotado
                            ? Icons.cancel
                            : Icons.check_circle_outline,
                        color: abrigo.estaLotado ? Colors.red : Colors.green,
                      ),
                    ],
                  ),
                ],
              ),
            ),
          );
        },
      ),
    );
  }
}
