# DNA-Project
This program starts with reading an inFile "Model.txt" and then generates a DNA sequence in an outFile "DNA.txt". Using a series of custom-generating methods, the program creates outFiles for translated RNA and Amino Acid sequences.

/////////////////////////////////////////////MAIN CODE START/////////////////////////////////////////////////////////////////////////////////////

package DNAproject;

import java.util.Scanner;
import java.util.Random;
import java.io.*;


public class project1 {

	
	public static void main(String[] args) throws FileNotFoundException {
		// TODO Auto-generated method stub
		
		Scanner inFile = new Scanner(new FileReader("Model.txt")); 
		PrintWriter outFileDNA = new PrintWriter("DNA.txt");
				
		String example = "";
		String parameters = "";
		String randseedUse = "";
		int randSeed = 0;
		String dnaTriples = "";
		String junk = "";
		int firstInt = 0;
		int secondInt = 0;
		
		example = inFile.nextLine();
		//System.out.println(example);
		parameters = inFile.nextLine();
		//System.out.println(parameters);
		randseedUse = inFile.nextLine();
		//System.out.println(randseedUse);
		randSeed = inFile.nextInt();
		junk = inFile.nextLine();
		//System.out.println(randSeed);
		dnaTriples = inFile.nextLine();
		//System.out.println(dnaTriples);
		firstInt = inFile.nextInt();
		junk = inFile.nextLine();
		//System.out.println(firstInt);
		secondInt = inFile.nextInt();
		//System.out.println(secondInt);
		inFile.close();
		
		/*System.out.println("DNA Base File");
		System.out.println(randseedUse);
		System.out.println(randSeed);
		System.out.println("DNA Base Sequences");
		System.out.println(generateSequence(firstInt));
		System.out.println(generateSequence(secondInt));*/
				
		outFileDNA.println("DNA Base File");
		outFileDNA.println(randseedUse);
		outFileDNA.println(randSeed);
		outFileDNA.println("DNA Base Sequences");
		String DNAsequence1 = "";
		String DNAsequence2 = "";
		String RNAsequence1 = "";
		String RNAsequence2 = "";
		
		DNAsequence1 = generateDNAsequence(firstInt);
		outFileDNA.println(DNAsequence1);
		DNAsequence2 = generateDNAsequence(secondInt);
		outFileDNA.println(DNAsequence2);
		outFileDNA.close();
		
		
			
		
		
		//Scanner inFileDNA = new Scanner(new FileReader("DNA.txt")); 
		PrintWriter outFileRNA = new PrintWriter("RNA.txt");
		
		
		outFileRNA.println("RNA File");
		outFileRNA.println(randseedUse);
		outFileRNA.println(randSeed);
		outFileRNA.println("mRNA Transcribed Sequences");
		outFileRNA.println(generateRNAsequence(DNAsequence1));	
		outFileRNA.println(generateRNAsequence(DNAsequence2));
		outFileRNA.close();
		
		//Scanner inFileRNA = new Scanner(new FileReader("RNA.txt")); 
		PrintWriter outFileAA = new PrintWriter("AA.txt");
		
		outFileAA.println("Amino Acid File");
		outFileAA.println(randseedUse);
		outFileAA.println(randSeed);
		outFileAA.println("Translated Amino Acid Sequences");
		outFileAA.println(generateAAsequence(DNAsequence1));
		outFileAA.println(generateAAsequence(DNAsequence2));
		outFileAA.close();
			
	}
	public static String generateDNAsequence(int myInt) {
		Random randgen = new Random();		
		String Adenine = "A";
		String Thymine = "T";
		String Cytosine = "C";
		String Guanine = "G";
		String newstr = "";
		int randInt = 0;
		int pairsofthree = 3;
		String sequence = "";
		for (int x=1; x <= myInt; x++) {
			for (int i = 0; pairsofthree > i; i++)
			{
				randInt = randgen.nextInt(4);
			
				if (randInt == 0)
				{
					newstr = Adenine;
				}
				else if (randInt == 1)
				{
					newstr = Thymine;
				}
				else if (randInt == 2)
				{
					newstr = Cytosine;
				}
				else if (randInt == 3)
				{
					newstr = Guanine;
				}
				sequence += newstr;
			
			}		
		}
		return sequence;
	}  // End of generateSequence
	public static String generateRNAsequence(String DNAstr) {
		String RNAstr = "";
		for(int j = 0; j<DNAstr.length(); j++) {
			if(DNAstr.charAt(j)=='A')
			{
				RNAstr += 'U';
			}
			else if(DNAstr.charAt(j)=='T') {
				RNAstr += 'A';
			}
			else if(DNAstr.charAt(j)=='G') {
				RNAstr += 'C';
			}
			else if(DNAstr.charAt(j)=='C') {
				RNAstr += 'G';
			}
			//else RNAstr += DNAstr.charAt(j);
			
		}
		return RNAstr;
	}

	public static String generateAAsequence(String seq) {
		String AAseq = "";
		String subSeq = new String("");
		int numofPairs = seq.length() / 3;
		int x = 0;
		//System.out.println(seq);
		for (int k = 0; k < numofPairs; k++) {
			subSeq = seq.substring(k+x, k+x + 3);
			if (subSeq.equals("ATA") || subSeq.equals("TAT") || subSeq.equals("CTT") || subSeq.equals("GAA")) {
				AAseq += "F";
				//System.out.println("F");
			}
			else if (subSeq.equals("GGG") || subSeq.equals("CCC") || subSeq.equals("ATT") || subSeq.equals("TAA")) {
				AAseq += "B";
				//System.out.println("B");
			}
			else if (subSeq.equals("CCG") || subSeq.equals("GGC")) {
				AAseq += "D";
				//System.out.println("D");
			}
			else if (subSeq.equals("GAC") || subSeq.equals("CTG") || subSeq.equals("GAG") || subSeq.equals("CTC")) {
				AAseq += "A";
				//System.out.println("A");
			}
			x += 2;
		}
		//System.out.println(AAseq);
		return AAseq;
	}
}
