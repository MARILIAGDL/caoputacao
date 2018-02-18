# caoputacao
cadastro e Login de um petshop ficticio,chamado Cãoputacão
using MySql.Data.MySqlClient;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace caoputacao
{
    class Program
    {

        private static ContatoDAO ContatoDao = new ContatoDAO();
        private static ProdutosDAO ProdutosDao = new ProdutosDAO();
        private static FuncionariosDAO FuncionariosDao = new FuncionariosDAO();
        private static ClientesDAO ClientesDao = new ClientesDAO();
        private static AnimaisDAO AnimaisDao = new AnimaisDAO();

        static void Main(string[] args)
        {
            MySqlConnection conexao = new MySqlConnection(@"server=localhost;user id=root;password=;database=caoputacao");
            try
            {
                conexao.Open();

                Console.WriteLine("Conexão realizada com sucesso!");
            }
            catch (Exception ex)
            {
                Console.WriteLine("Erro" + ex.Message);
            }
            finally
            {
                conexao.Close();
            }

            ExibirMenu();

        }

        static void ExibirMenu()
        {

            Console.Clear();
            Console.WriteLine("----- CÃOPUTACAO PETSHOP ----- ");
            Console.WriteLine("1 - Clientes");
            Console.WriteLine("2 - Animais");
            Console.WriteLine("3 - Produtos");
            Console.WriteLine("4 - Funcionários");
            Console.WriteLine("5 - Contato");
            Console.Write("Escolha uma opção:");

            int opcaoCaoputacao = int.Parse(Console.ReadLine());

            switch (opcaoCaoputacao)
            {
                case 1:
                    Console.WriteLine("----- CLIENTES ----- ");
                    Console.WriteLine("1 - Cadastrar cliente");
                    Console.WriteLine("2 - Alterar cliente");
                    Console.WriteLine("3 - Listar clientes");
                    Console.WriteLine("4 - Consultar cliente");
                    Console.Write("Escolha uma opção:");

                    int opcaoClientes = int.Parse(Console.ReadLine());

                    switch (opcaoClientes)
                    {
                        case 1:
                            CadastrarCliente();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 2:
                            AlterarCliente();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 3:
                            ListarClientes();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 4:
                            ConsultarCliente();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        default:
                            Console.WriteLine("Opção inválida!");
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                    }
                    break;

                case 2:
                    Console.WriteLine("----- ANIMAIS -----");
                    Console.WriteLine("1- Inserir animal");
                    Console.WriteLine("2 - Alterar animal");
                    Console.WriteLine("3 - Listar animal");
                    Console.WriteLine("4 - Consultar animal");
                    Console.Write("Escolha uma opção:");

                    int opcaoAnimais = int.Parse(Console.ReadLine());

                    switch (opcaoAnimais)
                    {
                        case 1:
                            InserirAnimal();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        case 2:
                            AlterarAnimal();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 3:
                            ListarAnimais();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 4:
                            ConsultarAnimal();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        default:
                            Console.WriteLine("Opção inválida!");
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                    }
                    break;

                case 3:
                    Console.WriteLine("----- PRODUTOS -----");
                    Console.WriteLine("1- Inserir produto");
                    Console.WriteLine("2 - Alterar produto");
                    Console.WriteLine("3 - Listar produtos");
                    Console.WriteLine("4 - Consultar produtos");
                    Console.Write("Escolha uma opção:");

                    int opcaoProdutos = int.Parse(Console.ReadLine());

                    switch (opcaoProdutos)
                    {
                        case 1:
                            InserirProduto();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        case 2:
                            AlterarProduto();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 3:
                            ListarProdutos();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 4:
                            ConsultarProduto();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        default:
                            Console.WriteLine("Opção inválida!");
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                    }
                    break;

                case 4:
                    Console.WriteLine("----- FUNCIONÁRIOS -----");
                    Console.WriteLine("1- Cadastrar funcionário");
                    Console.WriteLine("2 - Alterar funcionário");
                    Console.WriteLine("3 - Deletar funcionário");
                    Console.WriteLine("4 - Listar funcionário");
                    Console.WriteLine("5 - Consultar funcionário");
                    Console.Write("Escolha uma opção:");

                    int opcaoFuncionario = int.Parse(Console.ReadLine());

                    switch (opcaoFuncionario)
                    {
                        case 1:
                            InserirFuncionario();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        case 2:
                            AlterarFuncionario();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 3:
                            DeletarFuncionario();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 4:
                            ListarFuncionarios();
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                        case 5:
                            ConsultarFuncionario();
                            Console.ReadKey();
                            ExibirMenu();
                            break;

                        default:
                            Console.WriteLine("Opção inválida!");
                            Console.ReadKey();
                            ExibirMenu();
                            break;
                    }
                    break;

                case 5:
                    ListarContato();
                    Console.ReadKey();
                    ExibirMenu();
                    break;

                default:
                    Console.WriteLine("Opção inválida!");
                    Console.ReadKey();
                    ExibirMenu();
                    break;

            }
        }


        private static void InserirProduto()
        {
            int idProduto = 0;

            Console.WriteLine("Nome do Produto: ");
            string nomeProduto = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Preço do Produto: ");
            double precoProduto = double.Parse(Console.ReadLine());
            Console.ReadKey();

            Produtos produto = new Produtos(idProduto, nomeProduto, precoProduto);

            ProdutosDao.Inserir(produto);

            Console.WriteLine("Produto inserido!");
        }

        private static void AlterarProduto()
        {
            Console.WriteLine("ID do produto que deseja alterar: ");
            int idProduto = int.Parse(Console.ReadLine());
            Console.WriteLine("Novo nome do produto: ");
            string nomeProduto = Console.ReadLine();
            Console.WriteLine("Novo preço do produto: ");
            double precoProduto = double.Parse(Console.ReadLine());
            ProdutosDao.Alterar(nomeProduto, precoProduto, idProduto);
            Console.WriteLine("Produto alterado!");
        }

        private static void ListarProdutos()
        {
            ProdutosDao.ObterProdutos();
            List<Produtos> produtos = ProdutosDao.ObterProdutos();
            foreach (Produtos p in produtos)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Produto: {1}" + "\n" + "Preço: {2}" + "\n" + "----------", p.IdProduto, p.NomeProduto, p.PrecoProduto);
            }
        }

        private static void ConsultarProduto()
        {
            Console.WriteLine("ID do produto que deseja consultar: ");
            int idProduto = int.Parse(Console.ReadLine());
            ProdutosDao.ConsultarProdutos(idProduto);
            List<Produtos> produtos = ProdutosDao.ConsultarProdutos(idProduto);
            foreach (Produtos p in produtos)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Produto: {1}" + "\n" + "Preço: {2}" + "\n" + "----------", p.IdProduto, p.NomeProduto, p.PrecoProduto);
            }
        }

        private static void InserirFuncionario()
        {
            int idFuncionario = 0;

            Console.WriteLine("Nome do Funcionário: ");
            string nomeFuncionario = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Telefone do Funcionário: ");
            string telefoneFuncionario = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Salário do Funcionário: ");
            double salarioFuncionario = double.Parse(Console.ReadLine());
            Console.ReadKey();



            Funcionarios funcionario = new Funcionarios(idFuncionario, nomeFuncionario, telefoneFuncionario, salarioFuncionario);

            FuncionariosDao.Inserir(funcionario);

            Console.WriteLine("Funcionário inserido!");
        }

        private static void AlterarFuncionario()
        {
            Console.WriteLine("ID do funcionário que deseja alterar: ");
            int idFuncionario = int.Parse(Console.ReadLine());
            Console.WriteLine("Altualizar nome do funcionário: ");
            string nomeFuncionario = Console.ReadLine();
            Console.WriteLine("Atualizar telefone do Funcionário: ");
            string telefoneFuncionario = Console.ReadLine();
            Console.WriteLine("Atualizar salário do Funcionário: ");
            double salarioFuncionario = double.Parse(Console.ReadLine());
            FuncionariosDao.Alterar(idFuncionario, nomeFuncionario, telefoneFuncionario, salarioFuncionario);
            Console.WriteLine("Funcionário alterado!");
        }

        private static void DeletarFuncionario()
        {
            Console.WriteLine("ID do funcionário que deseja deletar: ");
            int idFuncionario = int.Parse(Console.ReadLine());
            FuncionariosDao.Deletar(idFuncionario);
            Console.WriteLine("Funcionário deletado!");
        }

        private static void ListarFuncionarios()
        {
            FuncionariosDao.ObterFuncionarios();
            List<Funcionarios> funcionarios = FuncionariosDao.ObterFuncionarios();
            foreach (Funcionarios f in funcionarios)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Funcionário: {1}" + "\n" + "Telefone: {2}" + "\n" + "Salário: {3}" + "\n" + "----------", f.IdFuncionario, f.NomeFuncionario, f.TelefoneFuncionario, f.SalarioFuncionario);
            }
        }

        private static void ConsultarFuncionario()
        {
            Console.WriteLine("ID do funcionário que deseja deletar: ");
            int idFuncionario = int.Parse(Console.ReadLine());
            FuncionariosDao.ConsultarFuncionarios(idFuncionario);
            List<Funcionarios> funcionarios = FuncionariosDao.ConsultarFuncionarios(idFuncionario);
            foreach (Funcionarios f in funcionarios)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Funcionário: {1}" + "\n" + "Telefone: {2}" + "\n" + "Salário: {3}" + "\n" + "----------", f.IdFuncionario, f.NomeFuncionario, f.TelefoneFuncionario, f.SalarioFuncionario);
            }
        }

        private static void CadastrarCliente()
        {
            Console.WriteLine("Nome do cliente: ");
            string nomeCliente = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Cpf do cliente: ");
            int cpfCliente = int.Parse(Console.ReadLine());
            Console.ReadKey();

            Console.WriteLine("Telefone do cliente: ");
            string telefoneCliente = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("ID do funcionário: ");
            int idFuncionario = int.Parse(Console.ReadLine());
            Console.ReadKey();


            Clientes cliente = new Clientes(cpfCliente, nomeCliente, telefoneCliente, idFuncionario);

            ClientesDao.Inserir(cliente);

            Console.WriteLine("Cliente inserido!");
        }

        private static void AlterarCliente()
        {
            Console.WriteLine("Cpf do cliente que deseja alterar: ");
            int cpfCliente = int.Parse(Console.ReadLine());
            Console.WriteLine("Novo nome do cliente: ");
            string nomeCliente = Console.ReadLine();
            Console.WriteLine("Novo telefone do cliente: ");
            string telefoneCliente = Console.ReadLine();
            Console.WriteLine("ID do funcionário: ");
            int idFuncionario = int.Parse(Console.ReadLine());
            ClientesDao.Alterar(nomeCliente, telefoneCliente, idFuncionario, cpfCliente);
            Console.WriteLine("Cliente alterado!");
        }

        private static void ListarClientes()
        {
            ClientesDao.ObterCliente();
            List<Clientes> cliente = ClientesDao.ObterCliente();
            foreach (Clientes c in cliente)
            {
                Console.WriteLine("----------" + "\n" + "CPF: {0}" + "\n" + "Cliente: {1}" + "\n" + "telefone: {2}" + "\n" + "ID Funcionário: {3}" + "\n" + "----------", c.CpfCliente, c.NomeCliente, c.TelefoneCliente, c.IdFuncionario);
            }
        }

        private static void ConsultarCliente()
        {
            Console.WriteLine("Cpf do cliente que deseja consultar: ");
            int cpfCliente = int.Parse(Console.ReadLine());
            ClientesDao.ConsultarCliente(cpfCliente);
            List<Clientes> cliente = ClientesDao.ConsultarCliente(cpfCliente);
            foreach (Clientes c in cliente)
            {
                Console.WriteLine("----------" + "\n" + "CPF: {0}" + "\n" + "Cliente: {1}" + "\n" + "Telefone: {2}" + "\n" + "ID Funcionário: {3}" + "\n" + "----------", c.CpfCliente, c.NomeCliente, c.TelefoneCliente, c.IdFuncionario);
            }
        }

        private static void InserirAnimal()
        {
            int idAnimal = 0;

            Console.WriteLine("Nome do Animal: ");
            string nomeAnimal = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Raça do animal: ");
            string racaAnimal = Console.ReadLine();
            Console.ReadKey();

            Console.WriteLine("Preço do serviço: ");
            double precoServicoAnimal = double.Parse(Console.ReadLine());
            Console.ReadKey();

            Console.WriteLine("CPF do Cliente: ");
            int cpfCliente = int.Parse(Console.ReadLine());
            Console.ReadKey();

            Animais animal = new Animais(idAnimal, nomeAnimal, racaAnimal, precoServicoAnimal, cpfCliente);

            AnimaisDao.Inserir(animal);

            Console.WriteLine("Animal inserido!");
        }

        private static void AlterarAnimal()
        {
            Console.WriteLine("ID do animal que deseja alterar: ");
            int idAnimal = int.Parse(Console.ReadLine());
            Console.WriteLine("Novo nome do animal: ");
            string nomeAnimal = Console.ReadLine();
            Console.WriteLine("Nova raça do animal: ");
            string racaAnimal = Console.ReadLine();
            Console.WriteLine("Novo preço do serviço: ");
            int precoServicoAnimal = int.Parse(Console.ReadLine());
            AnimaisDao.Alterar(nomeAnimal, racaAnimal, precoServicoAnimal, idAnimal);
            Console.WriteLine("Animal alterado!");
        }

        private static void ListarAnimais()
        {
            AnimaisDao.ObterAnimal();
            List<Animais> animal = AnimaisDao.ObterAnimal();
            foreach (Animais a in animal)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Nome: {1}" + "\n" + "Preço do serviço: {2}" + "\n" + "Raça: {3}" + "\n" + "CPF Cliente: {4}" + "\n" + "----------", a.IdAnimal, a.NomeAnimal, a.PrecoServicoAnimal, a.RacaAnimal, a.CpfCliente);
            }
        }

        private static void ConsultarAnimal()
        {
            Console.WriteLine("ID do animal que deseja consultar: ");
            int idAnimal = int.Parse(Console.ReadLine());
            AnimaisDao.ConsultarAnimal(idAnimal);
            List<Animais> animal = AnimaisDao.ConsultarAnimal(idAnimal);
            foreach (Animais a in animal)
            {
                Console.WriteLine("----------" + "\n" + "ID: {0}" + "\n" + "Nome: {1}" + "\n" + "Preço do serviço: {2}" + "\n" + "Raça: {3}" + "\n" + "CPF Cliente: {4}" + "\n" + "----------", a.IdAnimal, a.NomeAnimal, a.PrecoServicoAnimal, a.RacaAnimal, a.CpfCliente);
            }
        }

        private static void ListarContato()
        {
            ContatoDao.ObterEndereco();
            List<Contato> endereco = ContatoDao.ObterEndereco();
            Console.WriteLine("----- ENDERECOS -----");
            foreach (Contato c in endereco)
            {
                Console.WriteLine("{0}", c.Endereco);
            }
            ContatoDao.ObterTelefone();
            List<Contato> telefone = ContatoDao.ObterTelefone();
            Console.WriteLine("----- TELEFONES -----");
            foreach (Contato c in telefone)
            {
                Console.WriteLine("{0}", c.Telefone);
            }
            ContatoDao.ObterEmail();
            List<Contato> email = ContatoDao.ObterEmail();
            Console.WriteLine("----- EMAILS -----");
            foreach (Contato c in email)
            {
                Console.WriteLine("{0}", c.Email);
            }
        }
    }
}
