```cpp
/* Given a reference (pointer to pointer) to the head
of a list and an int, push a new node on the front
of the list. */
void push(Node** head_ref, int new_data)
{
    /* allocate node */
    Node* new_node = new Node();
    // What is the difference?
    // Node* new_node = (Node*)malloc(sizeof(Node));


    /* put in the data */
    new_node->data = new_data;

    /* link the old list of the new node */
    // Assigning value to next variable of new_node using arrow operator
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Main code*/
int main()
{
    /* Start with the empty list */
    Node* head = NULL;

    /* Use push() to construct linked list*/
    push(&head, 19);
    push(&head, 38);
    push(&head, 5);
    push(&head, 5);
    push(&head, 65);
    
    /* Count # of nodes */
    cout << "count of nodes is \n" << getCount(head) << "\n" << endl;
    printList(head);
    return 0;
}

