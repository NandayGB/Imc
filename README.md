# Imc
Imc 
var readlineSync = require('readline-sync'),
    fs = require('fs');
var historico = []
acoes = ['Novo', 'Ver historico']
console.log("Calculadora de IMC")
if (fs.existsSync("./imchistorico.json")) historico = require('./imchistorico.json')
ExibeOpcoes();

function ExibeOpcoes () {
    acaoEscolhida = readlineSync.keyInSelect(acoes, 'O que voce deseja fazer?');
    switch (acaoEscolhida) {
        case 0:
            NovoIMC();
            break;
        case 1:
            HistoricoIMC();
            break;
        default:
            break;
    }
}
function HistoricoIMC () {
    if(historico.length == 0) {
        console.log("O histórico está vazio")
    } else {
        for (let index = 0; index < historico.length; index++) {
            const item = historico[index];
            console.log(`${item.nome} | ${item.peso}kg | ${parseFloat(item.altura).toFixed(2)}m | ${item.classificacao}`)
        }
    }
    ExibeOpcoes();
}
function NovoIMC () {
    do {
        var nome = readlineSync.question(' Oi, qual o seu nome? ');
    } while (nome == "");

    
    do {
        var sobrenome = readlineSync.question('E o seu sobrenome? ');
    } while (sobrenome == "");
    do {
        var idade = readlineSync.question('Agora sua idade qual é? ');
    } while (idade == ""); console.log("Deve ser número")
    do {
        var peso = readlineSync.question('Que legal! Qual sexo você se define');
    } while (isNaN(sexo));

    do {
        var peso = readlineSync.question('Precisamos do seu e-mail para iniciar seu teste de imc, qual seria ele? ');
    } while (isNaN(e-mail));
    do {
        var peso = readlineSync.question('Qual o seu peso? ');
        if (isNaN(peso)) console.log("Deve ser número")
    } while (isNaN(peso));
    do {
        var altura = readlineSync.question('Qual a sua altura? ');
        if (isNaN(altura)) console.log("Deve ser número")
    } while (isNaN(altura));

    altura = altura > 2 ? altura / 100 : altura;
    var imc = peso / (altura * altura);
    var classificacao = "abaixo do peso";
    if (imc > 18.5) classificacao = imc > 18.5 && imc < 24.9 ? "peso normal" : "sobrepeso";

    console.log(`\r\nOlá ${nome},seu sobrenome é ${sobrenome}, a idade que possui é ${idade},o sexo que se declara é ${sexo} o e-mail utilizado para iniciar o teste é ${e-mail}, seu peso é ${peso} kg e a sua altura é ${parseFloat(altura).toFixed(2)}m, portanto o seu IMC é de ${parseFloat(imc).toFixed(2)} e é classificado como ${classificacao}.`);
    historico.push({
        nome, altura, peso, classificacao
    });
    fs.writeFile("imchistorico.json", JSON.stringify(historico), 'utf8', function (err) {
        if (err) {
            console.log("Erro ao salvar");
            return console.log(err);
        }
        ExibeOpcoes();
    });


} while (continuar == 'S');
console.log('\n Obrigada por consultar seu IMC em nossa pagína, até log.');
