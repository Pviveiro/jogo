jogo
====

Jogo de batalha naval em JAVA

import java.rmi.Naming;
import java.util.*;

public class BatalhaServidor {
	
	private Configuracao config = new Configuracao ();
	private ArrayList <Navio> NavioList = new ArrayList<Navio> ();
	
	private void iniciaJogo () {
		Navio um = new navio();
		Navio  dois= new navio();
		Navio  tres= new navio();
		NavioList.add(um);
		NavioList.add(dois);
		NavioList.add(tres);
		
		for (Navio lugarDoNavio : NavioList) { //repete para cada navio da lista
			ArrayList <string> localizacao = config.lugarNavio (3);
			lugarDoNavio.alterarLocaisDasCelulas (localizacao);
		}
		
	}
	
	private void  comecandoJogar () {
		
		while (!NavioList.isEmpty()) {
		
			String palpite = config.getPalpiteDoUsuario ("insira um palpite");
			
			checarpalpite (palpite);
			
		}
		fimDoJogo();
}
	
	private void checarpalpite (String palpite) {
		
		String resultadoDoPalpite = "errado";
		
		for (Navio testeDoAlvo: NavioList) {
			
			resultadoDoPalpite = testeDoAlvo.checar(palpite);
			
			if (resultadoDoPalpite.equals ("correto")) {
				
				break;
			}
			
			if(resultadoDoPalpite.equals("dstruido")) {
				
				NavioList.remove(testeDoAlvo);
				break;
			}
		}
	}

	private void fimDoJogo() {
		
		System.out.println("Você destruiu todos os navios do adversário");
	}
	
	public static void main (String []args) {
		
		BatalhaServidor jogo = new BatalhaServidor ();
		
		jogo.iniciaJogo();
		jogo.comecandoJogar();
		
		}
		
	}


