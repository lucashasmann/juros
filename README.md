📱 Descrição do Projeto
Você está desenvolvendo um aplicativo simulador de financiamento, que permite ao usuário calcular:

Valor da parcela mensal;

Montante total a ser pago no financiamento.

🧮 Entrada do usuário:
Valor do bem (ex: R$ 30.000);

Número de parcelas (ex: 36);

Taxa de juros mensal (ex: 1,5%);

Taxas adicionais (ex: seguro, tarifas bancárias).

📊 Cálculo feito com juros compostos:
Fórmula:
M = C × (1 + i)ᵗ
Onde:

M: Montante total a pagar;

C: Valor inicial (capital);

i: Taxa de juros mensal (em decimal);

t: Número de parcelas.

🛠️ Tecnologias Utilizadas
🔹 Dart
Linguagem principal do projeto. É usada para programar a lógica da simulação.

🔹 Flutter
Framework de UI (interface gráfica) para criar o app com entradas de dados, botões e resultado em tempo real.

🔹 Firebase
Usado para persistir dados (caso deseje salvar simulações), autenticar usuários, ou usar o Firestore para armazenar simulações anteriores.

🔹 Firebase Studio
Apesar de não existir oficialmente algo chamado "Firebase Studio", você deve estar se referindo ao console do Firebase em conjunto com o Flutter + Firebase CLI + Firebase Emulator.

⚙️ Como Executar o Projeto com Firebase e Flutter
1. ✅ Pré-requisitos
Flutter SDK instalado;

Dart SDK (incluso com Flutter);

Android Studio ou VSCode com Flutter Plugin;

Firebase CLI (npm install -g firebase-tools);

Conta no Firebase Console.

2. 🧪 Criar o projeto Flutter
bash
Copiar
Editar
flutter create simulador_financiamento
cd simulador_financiamento
3. 🔥 Integrar Firebase ao Flutter
a) Criar projeto no Firebase Console
Vá para console.firebase.google.com;

Clique em "Adicionar projeto";

Dê um nome ao projeto e avance sem Google Analytics.

b) Adicionar Firebase ao app Flutter
Clique em "Adicionar app" → "Android";

Pegue o nome do pacote no android/app/src/main/AndroidManifest.xml;

Siga os passos para adicionar o google-services.json;

No android/build.gradle, adicione:

gradle
Copiar
Editar
classpath 'com.google.gms:google-services:4.3.15'
No android/app/build.gradle, adicione no final:

gradle
Copiar
Editar
apply plugin: 'com.google.gms.google-services'
c) Adicionar pacotes no pubspec.yaml
yaml
Copiar
Editar
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.30.0
  cloud_firestore: ^4.14.0
d) Inicializar Firebase no app (main.dart)
dart
Copiar
Editar
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
4. 💻 Exemplo de lógica do cálculo
dart
Copiar
Editar
double calcularMontante(double capital, double taxaJuros, int parcelas) {
  return capital * pow((1 + taxaJuros), parcelas);
}

double calcularParcelaMensal(double montante, int parcelas) {
  return montante / parcelas;
}
5. ☁️ (Opcional) Salvar simulações no Firebase Firestore
dart
Copiar
Editar
FirebaseFirestore.instance.collection('simulacoes').add({
  'valor': capital,
  'taxa': taxaJuros,
  'parcelas': parcelas,
  'montante': montante,
  'data': Timestamp.now(),
});
6. ▶️ Executar o app
bash
Copiar
Editar
flutter run
