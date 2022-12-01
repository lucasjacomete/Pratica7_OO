package br.com.pratica7;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class PesquisaLivro {
 
  private static final String SELECT_LIVROS_BY_PRECO_SQL = "SELECT id_isbn, id_categoria, id_editora, nm_titulo, dt_publicacao, nu_edicao, nu_volume, vl_preco FROM livro WHERE vl_preco = ?";
  private static final String SELECT_LIVROS_BY_TITULO_SQL = "SELECT id_isbn, id_categoria, id_editora, nm_titulo, dt_publicacao, nu_edicao, nu_volume, vl_preco FROM livro WHERE nm_titulo like ?";
 
  public PesquisaLivro() {
    
  }

  public String selectRecordByPreco(double vl_preco) throws SQLException {
    Connection conn = ConexaoPostgre.connect();
    String str = "";
    try {
      PreparedStatement pstmt = conn.prepareStatement(SELECT_LIVROS_BY_PRECO_SQL);
      pstmt.setDouble(1, vl_preco);
      ResultSet rs = pstmt.executeQuery();
      while (rs.next()) {
        String id_isbn = rs.getString("id_isbn");
        String nm_titulo = rs.getString("nm_titulo");
        String preco = rs.getString("vl_preco");
        str = "ISBN: " + id_isbn + "\nTitulo: " + nm_titulo + "\nPreço: " + preco;
      }
    } catch (SQLException e) {
      ConexaoPostgre.printSQLException(e);
    }
    conn.close();
    return str;
  }
  
  public String selectRecordByTitulo(String nm_titulo) throws SQLException {
    Connection conn = ConexaoPostgre.connect();
    String str = "";
    try {
      PreparedStatement pstmt = conn.prepareStatement(SELECT_LIVROS_BY_TITULO_SQL);
      pstmt.setString(1, nm_titulo + "%");
      ResultSet rs = pstmt.executeQuery();
      while (rs.next()) {
        String id_isbn = rs.getString("id_isbn");
        String titulo = rs.getString("nm_titulo");
        String preco = rs.getString("vl_preco");
        str = "ISBN: " + id_isbn + "\nTitulo: " + titulo + "\nPreço: " + preco;
      }
    } catch (SQLException e) {
      ConexaoPostgre.printSQLException(e);
    }
    conn.close();
    return str;
  }
}