#include <stdio.h>

#include <stdlib.h>

struct node

{

	char data;

	struct node* next;

};

void push(struct node** top_ref, int new_data);

int pop(struct node** top_ref);

int matching(char ch1, char ch2)

{

	if (ch1 == '(' && ch2 == ')')

		return 1;

	else if (ch1 == '{' && ch2 == '}')

		return 1;

	else if (ch1 == '[' && ch2 == ']')

		return 1;

	else

		return 0;

}

int areBracketsBalanced(char exp[])

{

	int i = 0;

	struct node* stack = NULL;

	while (exp[i])

	{

		if (exp[i] == '{' || exp[i] == '(' || exp[i] == '[')

			push(&stack, exp[i]);

		if (exp[i] == '}' || exp[i] == ')'

			|| exp[i] == ']') 

		{

			if (stack == NULL)

				return 0;

			else if (!matching(pop(&stack), exp[i]))

				return 0;

		}

		i++;

	}

	if (stack == NULL)

		return 1; // balanced

	else

		return 0; // not balanced

}

int main()

{

	char exp[100];

	scanf("%s",exp);

	if (areBracketsBalanced(exp))

		printf("Balanced \n");

	else

		printf("Not Balanced \n");

	return 0;

}

void push(struct node** top_ref, int new_data)

{

	// allocate node

	struct node* new_node=(struct node*)malloc(sizeof(struct node));

	if (new_node == NULL) 

	{

		printf("Stack overflow n");

		getchar();

		exit(0);

	}

	new_node->data = new_data;

	new_node->next = (*top_ref);

	(*top_ref) = new_node;

}

int pop(struct node** top_ref)

{

	char res;

	struct node* top;

	// If stack is empty then error

	if (*top_ref == NULL) 

	{

		printf("Stack overflow n");

		getchar();

		exit(0);

	}

	else 

	{

		top = *top_ref;

		res = top->data;

		*top_ref = top->next;

		free(top);

		return res;

	}

	}
