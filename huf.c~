#include <stdio.h>
#include <stdlib.h>

struct Node {
    float prob;
    struct Node* nextnode, *leftnode, *rightnode;     
};

int ListLength(struct Node *);
void PrintResult(struct Node *,char *,int);
void FreeTree(struct Node *);

int main() {
  
    struct Node* headnode = NULL, *newnode = NULL, *lastnode = NULL, *curnode = NULL, *prenode = NULL;
    struct Node* min1node = NULL, *min2node = NULL;
    char* CodeString = NULL;
    char FileName [100] = "./test.txt";
    int CharNumber;
    float receive, MinProb;
    
    FILE *fptr = fopen(FileName, "r");
    
    fscanf(fptr, "%d ", &CharNumber);
    
    headnode = (struct Node*)calloc(sizeof(struct Node), 1);
    
    fscanf(fptr,"%f ", &(headnode->prob));
    
    lastnode = headnode;
    
    while(fscanf(fptr, "%f ", &receive) == 1) {
        newnode = (struct Node* ) calloc(sizeof(struct Node), 1);
        newnode -> prob = receive;
        lastnode -> nextnode = newnode;
        lastnode = newnode;
    }
    
    fclose(fptr);
    
    //print input data
    printf("Input:");	
    curnode = headnode;
    while(curnode != NULL) {
        printf("%.2f ", curnode -> prob);
    	curnode = curnode -> nextnode;
    }
    printf("\n");
    
    //huffman code
    while(ListLength(headnode) != 1) {
        MinProb = 2.0;
        curnode = headnode;
        while(curnode != NULL) {
            if ((curnode -> prob) < MinProb) {
                MinProb = curnode -> prob;
                min1node = curnode;
            }
   	    curnode = curnode -> nextnode;     
        }
        
        MinProb = 2.0;
        curnode = headnode;
        while (curnode != NULL) {
            if ((curnode -> prob) < MinProb && curnode != min1node) {
                MinProb = curnode -> prob;            
                min2node = curnode;
            }
            curnode = curnode -> nextnode;
        }
        
        newnode = (struct Node*) calloc (sizeof (struct Node), 1);
        newnode -> prob = (min1node -> prob) + (min2node -> prob);
        newnode -> leftnode = min1node;
        newnode -> rightnode = min2node;
        
        //add to the front
        newnode -> nextnode = headnode;
        
        //remove 2 minimal node
    	prenode = headnode;
    	curnode = headnode -> nextnode;
    	while (curnode != NULL) {
    	    if (curnode == min1node || curnode == min2node) {
    	        prenode -> nextnode = curnode -> nextnode;
    	        curnode -> nextnode = NULL;
    	        curnode = prenode;
    	    }
    	    prenode = curnode;
    	    curnode = curnode -> nextnode;
    	}
    }
    	CodeString = (char* ) malloc (sizeof (char)* CharNumber);
    	PrintResult(headnode, CodeString, 0);
    	
    	FreeTree(headnode);
    	free(CodeString);
    	
    	printf("\n");
    	
}

int ListLength(struct Node* headnode) {
    struct Node* curnode = NULL;
    int length;
    length = 0;
    curnode = headnode;
    while(curnode != NULL) {
        length++;
        curnode = curnode->nextnode;
    }
    return length;
}

void PrintResult(struct Node* startnode, char* codestring, int level) {
    if ((startnode -> leftnode) != NULL) {
        codestring[level] = '0';
        PrintResult(startnode -> leftnode, codestring, level+1);
        codestring[level]= '1';
        PrintResult(startnode -> rightnode, codestring, level+1);
    } else {
        printf("%.2f => ", startnode -> prob);
        codestring[level] = '\0';
        printf("%s\n", codestring);
    }
 
}

void FreeTree(struct Node* startnode) {
    if (startnode != NULL) {
        FreeTree(startnode -> leftnode);
        FreeTree(startnode -> rightnode);
        free(startnode);
    }
}
