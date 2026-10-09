<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Você decide o futuro da IA</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #080b20, #172554, #312e81);
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .caixa-principal {
            background: rgba(15, 23, 42, 0.95);
            width: 100%;
            max-width: 750px;
            padding: 35px;
            border-radius: 20px;
            border: 1px solid #6366f1;
            box-shadow: 0 0 35px rgba(99, 102, 241, 0.3);
        }

        h1 {
            text-align: center;
            color: #a5b4fc;
            margin-bottom: 25px;
            font-size: 2rem;
        }

        p {
            font-size: 1.05rem;
            line-height: 1.8;
            margin-bottom: 25px;
            color: #e2e8f0;
        }

        button {
            background: #6366f1;
            color: white;
            border: none;
            padding: 14px 22px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: 0.3s;
        }

        button:hover {
            background: #818cf8;
            transform: translateY(-2px);
        }

        .iniciar-btn,
        .novamente-btn {
            display: block;
            margin: 0 auto;
            width: 100%;
        }

        .caixa-perguntas,
        .caixa-alternativas,
        .caixa-resultado {
            display: none;
        }

        .mostrar {
            display: block;
            animation: aparecer 0.5s ease;
        }

        .caixa-perguntas {
            font-size: 1.35rem;
            font-weight: bold;
            line-height: 1.6;
            color: #c7d2fe;
            margin-bottom: 25px;
        }

        .caixa-alternativas {
            display: none;
            gap: 12px;
        }

        .caixa-alternativas.mostrar {
            display: flex;
            flex-direction: column;
        }

        .caixa-alternativas button {
            width: 100%;
            text-align: left;
            background: #1e293b;
            border: 1px solid #475569;
            font-weight: normal;
            line-height: 1.5;
        }

        .caixa-alternativas button:hover {
            background: #3730a3;
            border-color: #a5b4fc;
        }

        .caixa-resultado {
            text-align: center;
        }

        .caixa-resultado h2 {
            color: #a5b4fc;
            margin-bottom: 20px;
        }

        .progresso {
            height: 8px;
            background: #334155;
            border-radius: 10px;
            margin-bottom: 25px;
            overflow: hidden;
        }

        .barra-progresso {
            height: 100%;
            width: 0%;
            background: #818cf8;
            transition: width 0.3s;
        }

        .contador {
            text-align: right;
            color: #94a3b8;
            font-size: 0.85rem;
            margin-bottom: 10px;
        }

        @keyframes aparecer {
            from {
                opacity: 0;
                transform: translateY(10px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 500px) {
            .caixa-principal {
                padding: 22px;
            }

            h1 {
                font-size: 1.6rem;
            }

            .caixa-perguntas {
                font-size: 1.15rem;
            }
        }
    </style>
</head>

<body>

    <main class="caixa-principal">
        <h1>Você decide o futuro da IA</h1>

        <section class="tela-inicial">
            <p>
                Novembro de 2022, a humanidade se viu em uma realidade
                perturbadora. De repente, percebemos que as máquinas
                evoluíram para além do que imaginávamos.

                Agora, elas escrevem e falam de um jeito tão parecido
                com humanos que é quase impossível diferenciar quem
                foi que escreveu ou falou o quê.

                Em meio a esse caos de identidade, uma missão surgiu.

                Nosso objetivo: explorar o impacto da Inteligência
                Artificial (IA) em nossas vidas e confrontar as
                possibilidades que o futuro nos reserva.

                O mundo nunca mais será o mesmo.
            </p>

            <button class="iniciar-btn">Iniciar</button>
        </section>

        <section class="jogo">
            <div class="contador"></div>

            <div class="progresso">
                <div class="barra-progresso"></div>
            </div>

            <div class="caixa-perguntas"></div>
            <div class="caixa-alternativas"></div>
        </section>

        <section class="caixa-resultado">
            <h2>O futuro está em suas mãos!</h2>
            <p class="texto-resultado"></p>
            <button class="novamente-btn">Jogar novamente</button>
        </section>
    </main>

    <script>
        const telaInicial = document.querySelector(".tela-inicial");
        const telaJogo = document.querySelector(".jogo");
        const caixaPerguntas = document.querySelector(".caixa-perguntas");
        const caixaAlternativas = document.querySelector(".caixa-alternativas");
        const caixaResultado = document.querySelector(".caixa-resultado");
        const textoResultado = document.querySelector(".texto-resultado");
        const botaoIniciar = document.querySelector(".iniciar-btn");
        const botaoNovamente = document.querySelector(".novamente-btn");
        const contador = document.querySelector(".contador");
        const barraProgresso = document.querySelector(".barra-progresso");

        const perguntas = [
            {
                pergunta: "1. Uma inteligência artificial começa a realizar tarefas melhor do que os humanos. O que você faria?",
                alternativas: [
                    {
                        texto: "Usaria a IA para facilitar tarefas e aumentar a produtividade.",
                        pontos: 2
                    },
                    {
                        texto: "Permitiria seu uso, mas com supervisão humana.",
                        pontos: 3
                    },
                    {
                        texto: "Evitaria a tecnologia por medo de perder o controle.",
                        pontos: 1
                    }
                ]
            },
            {
                pergunta: "2. Uma escola decide permitir que alunos utilizem IA nos trabalhos. Qual seria sua opinião?",
                alternativas: [
                    {
                        texto: "A IA deveria fazer todos os trabalhos para os alunos.",
                        pontos: 1
                    },
                    {
                        texto: "Os alunos poderiam usar IA como ferramenta de aprendizado.",
                        pontos: 3
                    },
                    {
                        texto: "A IA deveria ser proibida em todas as atividades escolares.",
                        pontos: 2
                    }
                ]
            },
            {
                pergunta: "3. Uma empresa utiliza IA para selecionar candidatos a empregos. O que deveria acontecer?",
                alternativas: [
                    {
                        texto: "Deixar a IA decidir sozinha quem será contratado.",
                        pontos: 1
                    },
                    {
                        texto: "Usar a IA como apoio, com revisão humana e critérios transparentes.",
                        pontos: 3
                    },
                    {
                        texto: "Proibir qualquer uso de IA em processos seletivos.",
                        pontos: 2
                    }
                ]
            },
            {
                pergunta: "4. Uma IA cria notícias falsas muito convincentes. Como a sociedade deveria reagir?",
                alternativas: [
                    {
                        texto: "Investir em educação digital e verificação das informações.",
                        pontos: 3
                    },
                    {
                        texto: "Confiar nas notícias que parecem verdadeiras.",
                        pontos: 1
                    },
                    {
                        texto: "Proibir toda ferramenta capaz de gerar textos e imagens.",
                        pontos: 2
                    }
                ]
            },
            {
                pergunta: "5. No futuro, robôs e IA poderão realizar muitas atividades profissionais. Qual seria a melhor solução?",
                alternativas: [
                    {
                        texto: "Deixar que a tecnologia substitua os trabalhadores sem mudanças.",
                        pontos: 1
                    },
                    {
                        texto: "Investir em educação, capacitação e novas oportunidades de trabalho.",
                        pontos: 3
                    },
                    {
                        texto: "Impedir qualquer avanço tecnológico que automatize tarefas.",
                        pontos: 2
                    }
                ]
            }
        ];

        let atual = 0;
        let pontuacao = 0;

        function iniciaJogo() {
            atual = 0;
            pontuacao = 0;

            telaInicial.style.display = "none";
            caixaResultado.classList.remove("mostrar");
            telaJogo.style.display = "block";

            mostraPergunta();
        }

        function mostraPergunta() {
            caixaAlternativas.innerHTML = "";

            if (atual >= perguntas.length) {
                mostraResultado();
                return;
            }

            const perguntaAtual = perguntas[atual];

            contador.textContent =
                `Pergunta ${atual + 1} de ${perguntas.length}`;

            barraProgresso.style.width =
                `${(atual / perguntas.length) * 100}%`;

            caixaPerguntas.textContent = perguntaAtual.pergunta;

            perguntaAtual.alternativas.forEach((alternativa) => {
                const botao = document.createElement("button");

                botao.textContent = alternativa.texto;

                botao.addEventListener("click", () => {
                    pontuacao += alternativa.pontos;
                    atual++;
                    mostraPergunta();
                });

                caixaAlternativas.appendChild(botao);
            });
        }

        function mostraResultado() {
            telaJogo.style.display = "none";
            caixaResultado.classList.add("mostrar");
            barraProgresso.style.width = "100%";

            let titulo = "";
            let mensagem = "";

            if (pontuacao >= 13) {
                titulo = "Você é um agente do futuro responsável!";
                mensagem =
                    "Suas escolhas mostram que você valoriza o potencial da IA, " +
                    "sem esquecer a importância da responsabilidade, da educação " +
                    "e da supervisão humana. Você acredita que a tecnologia pode " +
                    "ajudar a construir um futuro melhor quando usada com cuidado.";
            } else if (pontuacao >= 9) {
                titulo = "Você busca equilíbrio!";
                mensagem =
                    "Você reconhece que a inteligência artificial traz benefícios, " +
                    "mas também apresenta riscos. Seu desafio será encontrar o " +
                    "equilíbrio entre inovação, segurança e participação humana.";
            } else {
                titulo = "O futuro exige reflexão!";
                mensagem =
                    "Suas escolhas mostram que existem desafios importantes na " +
                    "relação entre humanos e inteligência artificial. Refletir " +
                    "sobre as consequências da tecnologia é um primeiro passo " +
                    "para decidir como queremos construir o futuro.";
            }

            caixaResultado.querySelector("h2").textContent = titulo;
            textoResultado.textContent =
                mensagem + ` Sua pontuação foi ${pontuacao} de 15.`;
        }

        function jogarNovamente() {
            telaInicial.style.display = "block";
            telaJogo.style.display = "none";
            caixaResultado.classList.remove("mostrar");
            barraProgresso.style.width = "0%";
        }

        botaoIniciar.addEventListener("click", iniciaJogo);
        botaoNovamente.addEventListener("click", jogarNovamente);

        telaJogo.style.display = "none";
    </script>

</body>
</html>
