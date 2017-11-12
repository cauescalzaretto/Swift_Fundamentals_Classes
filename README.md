# Swift Fundamentals Classes

    //: Playground - noun: a place where people can play
    
    import UIKit
    
    
    //---------------------------------------------------------------
    //: Author - Cauê Scalzaretto
    //: Site - http://www.cauescalzaretto.com
    //: GitHub - https://github.com/cauescalzaretto
    //---------------------------------------------------------------
    
    
    
    //Principais Conceitos:
    //
    //  - abstração de objetos que possuem caracteríticas semelhantes;
    //  - herdar métodos, propriedades e outras caracterísitcas de outra classe;
    //  - reutilização de código !
    //
    //
    //Sintaxe:
    //
    //class NomeDaClasse : SuperClasseHerdada{
    //    // Definição da classe com propriedades e métodos
    //}
    
    
    //---------------------------------------------------------------
    
    //Criando a classe
    class Carro { }
    
    //Utilizando a classe para definir tipo do objeto
    let fusca = Carro()
    let uno = Carro()
    let camaro = Carro()
    
    
    //=======================================================================================================================
    // PROPRIEDADES ou atributos, são as características de um objeto definidas dentro do escopo de uma classe.
    //
    // MÉTODOS efetuam alguma ação e podem ou não devolver um resultado
    //=======================================================================================================================
    
    //Criando a classe Animal
    class Animal {
        
        //Declaração de propriedades
        var peso: Double = 0.0
        var altura: Double = 0.0
        var idade: Int = 0
        
        // Declaração dos métodos
        func comer(){
            print("Animal comendo")
        }
        
    } //Fechamento do escopo da classe
    
    // Instanciando o objeto passaro
    var passaro = Animal()
    
    // Utilizando o método
    passaro.comer()
    
    // Definindo as propriedades do objeto passaro
    passaro.peso = 0.5
    passaro.idade = 1
    
    
    //=======================================================================================================================
    // ENCAPSULAMENTO
    //
    //  - public    -> permite acesso a um elemento da classe
    //  - internal  -> permite acesso somente ao próprio pacote (bundle)
    //  - private   -> permite acesso apenas dentro da classe onde foi declarada
    //=======================================================================================================================
    
    //Arquivo da Classe:
    class Pessoa {
        
        // Declaração de propriedades
        var nome: String = ""
        // Propriedade que será acessada através de métodos
        private var idade: Int = 0
        
        // Méetodo que altera a idade
        func mudarIdade(novaIdade: Int)
        {
            idade = novaIdade
        }
        
        // Método que retorna a idade
        func imprimeIdade()
        {
            print("Idade: \(idade)")
        }
        
        internal func saudacao() -> String
        {
            return "Olá \(nome) ! Você tem \(idade) anos de vida !"
        }
        
    }
    
    // Instanciando o objeto humano
    var humano = Pessoa()
    
    humano.nome = "Cauê"
    
    // Usando o método para acessar idade
    humano.mudarIdade(novaIdade: 40)
    
    humano.imprimeIdade()
    
    print(humano.saudacao())
    
    Pessoa().saudacao()
    
    //=======================================================================================================================
    // MÉTODOS INICIALIZADORES
    //
    //  - Inicializadores permitem que ao se instanciar uma classe, determinadas ações sejam realizadas
    //=======================================================================================================================
    
    // EXEMPLO 1
    class Celsius
    {
        var temperatura: Double = 0.0
    
        init()
        {
            temperatura = 25.0
        }
    }
    
    // EXEMPLO 2
    class Conversor_de_Fahrenheit_para_Celsius
    {
        var temperatura: Double = 0.0
    
        init(valorFahrenheit: Double)
        {
            temperatura = (valorFahrenheit - 32.0) / 1.8
        }
    
    }
    
    let converterTemperatura = Conversor_de_Fahrenheit_para_Celsius(valorFahrenheit: 37.0)
    print(converterTemperatura.temperatura)
    
    
    //=======================================================================================================================
    // HERANÇA
    //
    //  - A herança permite que se crie classe, herdando as funcionalidades pertencentes a outra classa
    //
    //=======================================================================================================================
    
    // Criando a classe Roda
    class Roda {
        
        // Declaração de propriedades
        var raio: Double = 0.0
        
        // Inicializa a classe
        init(raioDaRoda: Double)
        {
            raio = raioDaRoda
        }
        
        // Método da classe
        func retornaRaioDaRoda() -> String
        {
            return "Raio: \(raio)"
        }
    
    }
    
    // Criando a classe RodaAutomotiva e herdando as propriedades e métodos da classe Roda
    class RodaAutomotiva: Roda
    {
        // Declaração de propriedades
        var tala: Double = 0.0
        var quantidadeFuracao: Int = 0
        var distanciaFuros: Double = 0.0
        
        // Inicializa a classe
        init(talaDaRoda: Double, qtdeFurosDaRoda: Int, distFurosDaRoda: Double,raioDaRodaAutomotiva: Double)
        {
            tala = talaDaRoda
            quantidadeFuracao = qtdeFurosDaRoda
            distanciaFuros = distFurosDaRoda
            
            // É OBRIGATÓRIO DECLARAR O INICIALIZADOR DA CLASSE HERDADA
            super.init(raioDaRoda: raioDaRodaAutomotiva)
        }
        
        
    }
    
    // Instanciando a classe
    let minhaRodaAutomotiva = RodaAutomotiva(talaDaRoda: 5.5, qtdeFurosDaRoda: 4, distFurosDaRoda: 108.0, raioDaRodaAutomotiva: 14)
    
    print(minhaRodaAutomotiva.retornaRaioDaRoda())
    
    
    //=======================================================================================================================
    // WILLSET / DIDSET
    //
    // - São objetos OBSERVER, que são executados quando uma propriedade é acessada
    //=======================================================================================================================
    
    class Abastecer {
        
        // Declaração de propriedades
        var contador : Int = Int()
        {
            // Será EXECUTADA APÓS a propriedade contador ser alterada
            willSet(novaContagem)
            {
                print("Abastercer \(novaContagem) litros!")
            }
            
            // Será EXECUTADA ANTES da propriedade contador ser alterada
            didSet
            {
                let novoValor = oldValue
        
                if contador > novoValor
                {
                    print("Abasteceu \(contador + novoValor) litros")
                }
            }
        }
    }
    
    // Instanciando a classe
    let abastecendoMeuCarro = Abastecer()
    
    abastecendoMeuCarro.contador = 10
    
    
    
    //=======================================================================================================================
    // LAZY
    //
    // - Utilizado quando queremos retardar a criação de um objeto ou processo
    // - UTILIZE COM SABEDORIA !
    //=======================================================================================================================
    
    class Doces
    {
        // Declaração de propriedades
        var nomeDoce = String()
    }
    
    class PratoPrincipal
    {
        // Declaração de propriedades
        var nomePrato = String()
    }
    
    class Entrada
    {
        // Declaração de propriedades
        var nomeEntrada = String()
    }
    
    
    // Classe Refeicao
    class Refeicao {
     
        // A variável sobremesa e pratoPrinciapl não serão criadas no momento que a instância for declarada
        lazy var sobremesa = Doces()
        lazy var pratoPrincipal = PratoPrincipal()
        
        var entrada = Entrada()
        
    }
    
    // Neste momento somente a variável entrada foi criada
    var minhaRefeicao = Refeicao()
    
    // Atribuindo um valor no atributo entrada
    minhaRefeicao.entrada.nomeEntrada = "Salada"
    
    // Neste momento ao acessar o atributo pratoPrincipal, tudo é inicializado....
    minhaRefeicao.pratoPrincipal.nomePrato = "Truta Salmonada com Mousse de Camarão"
    
    
    //=======================================================================================================================
    // SOBRECARGA
    //
    // - Permite que um método possa ser acessado definindo ou não novos parâmetros, com os mesmos retornos ou novos retornos
    //
    //=======================================================================================================================
    
    class Saudacao
    {
        // Declaração de propriedades
        var texto: String
        
        // Criando o inicializador e definindo um valor para a propriedade texto
        init()
        {
            texto = "Olá !"
        }
        
        // Criando a SOBRECARGA do método inicializador
        init(meuTexto: String)
        {
            texto = meuTexto
        }
        
        // Método que imprimie o texto
        func retornaSaudacao()
        {
            print("\(texto)")
        }
        
        // Método que retorna o texto, mas em SOBRECARGA
        func retornaSaudacao() -> String
        {
            return texto
        }
        
        
    }

