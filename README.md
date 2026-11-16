//Gustavo Augusto Silva de Queiroz
//RA: 0025065
package Crudnuvem;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Scanner;

public class Projeto {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		// conexao local
		//mysql://root:FBcRVwkKkwVFvSkVUtxjAMLLVObJSsgw@viaduct.proxy.rlwy.net:48773/railway
		String url = "jdbc:mysql://viaduct.proxy.rlwy.net:48773/railway";
		String usuariobanco= "root";
		String bancosenha= "FBcRVwkKkwVFvSkVUtxjAMLLVObJSsgw";
	
		/*
		//banco no ceu
		
		String url = "mysql://root:VJmgeVRkroiTTrhqiyDbmQHiGIlFINWA@mysql.railway.internal:3306/railway";
		String usuariobanco= "root";
		String bancosenha= "VJmgeVRkroiTTrhqiyDbmQHiGIlFINWA";
		*/
		
		//conexao no ceu
		
	Scanner sc= new Scanner(System.in);
	try {
		
		Connection conexao = DriverManager.getConnection(url, usuariobanco, bancosenha);
		
		int opcao = -1;
				
		while(opcao != 0) {
			System.out.println(" 1 - Inserir| 2- listar | 3- atualizar | 5 - deletar | 0 - sair");
			opcao = sc.nextInt();
			
			switch(opcao) {
			case 1: 
				System.out.print("Código do produto: ");
				int codigo = sc.nextInt();
				
				System.out.println("Nome do Produto: ");
				String nome =sc.next();
				
				System.out.println("Preço do produto: ");
				float preco =sc.nextFloat();
				
				String sql = "INSERT INTO PRODUTO(CODIGO,NOME,PRECO) VALUES(?,?,?)";
				
				PreparedStatement stmt= conexao.prepareStatement(sql);
				stmt.setInt(1, codigo);
				stmt.setString(2, nome);
				stmt.setFloat(3, preco);
				stmt.executeUpdate();
				System.out.println("Registro inserido com sucesso");
				break;
				
			case 2:
				System.out.println("Digite o códido do usuario");
				int codigo2 = sc.nextInt();
				
				String sql2 = " SELECT * FROM PRODUTO WHERE CODIGO = ? ";
				PreparedStatement stmt2 = conexao.prepareStatement(sql2);
				
				stmt2.setInt(1, codigo2);
				ResultSet rs=stmt2.executeQuery();
				while(rs.next()) {
					System.out.println("Nome Produto:"+ rs.getString("nome")+
							"Preço: "+ rs.getFloat("preco"));
	
				}
				break;
				
			case 3: 
				System.out.println( "Digite o codigo do produto para atualizar:" );
				int codPesquisa = sc.nextInt();
				
				System.out.print("Digite o novo preço do produto : ");
				float novopreco = sc.nextFloat();
				
				String sqlUpd = "UPDATE PRODUTO SET PRECO = ? WHERE CODIGO= ?";
				
				PreparedStatement stmtUp = conexao.prepareStatement(sqlUpd);
				stmtUp.setFloat(1, novopreco);
				stmtUp.setInt(2, codPesquisa);
				
				
				int linhaAfetada = stmtUp.executeUpdate();
				
				if(linhaAfetada > 0) {
					System.out.println("Preço Atualizado com Sucesso");
				}else {
					System.out.println("Produto não localizado");
				}
				break;
				
			case 4:
				System.out.println( "Digite o codigo do produto para deletar:" );
				int coddelete = sc.nextInt();
				
				
				String sqlDel = "DELETE FROM PRODUTO WHERE CODIGO = ? ";
				
				PreparedStatement stmtDele = conexao.prepareStatement(sqlDel);
				stmtDele.setInt(1, coddelete);
				
			
				int linhaAfetada2 = stmtDele.executeUpdate();
				
				if(linhaAfetada2 > 0) {
					System.out.println("Deletado com Sucesso");
				}else {
					System.out.println("Produto não localizado");
				}
				break;
				
			
				
			default:
				System.out.println("Opção Invalida");
				
			}
			
		}
		
		
		
		
		
		}catch(Exception e){
			
			System.out.println("Erro de Cadastro"+e.getMessage());
			
		}
		
	}
	
	
	

	}
