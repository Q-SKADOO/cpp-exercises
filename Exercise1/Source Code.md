```cpp
// Iterative C++ program to find length
// or count of nodes in a linked list
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
class Node {
public:
    int data;

    Node* next;
};


/* Set of Function Julio Requested*/


// Insert one additional rectangle on list. Front, back or middle

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



void deleteNode(Node** head, int position)
{
    Node* temp;
    Node* prev;
    temp = *head;
    prev = *head;

    for (int i = 0; i < position; i++) {
        if (i == 0 && position == 1) {
            *head = (*head)->next;
            free(temp);
        }
        else {
            if (i == position - 1 && temp) {
                prev->next = temp->next;
                free(temp);
            }
            else {
                prev = temp;

                // Position was greater than
                // number of nodes in the list
                if (prev == NULL)


                    break;
                temp = temp->next;
            }
        }
    }
}

/* Function to remove the last node
   of the linked list */
Node* removeLastNode(struct Node* head)
{
    if (head == NULL)
        return NULL;

    if (head->next == NULL) {
        delete head;
        return NULL;
    }

    // Find the second last node
    Node* second_last = head;
    while (second_last->next->next != NULL)
        second_last = second_last->next;

    // Delete last node
    delete (second_last->next);

    // Change next of second last
    second_last->next = NULL;

    return head;
}

/* Function to remove the first node
   of the linked list */
Node* removeFirstNode(struct Node* head)
{
    if (head == NULL)
        return NULL;

    // Move the head pointer to the next node
    Node* temp = head;
    head = head->next;

    delete temp;

    return head;
}


/* Checks whether the value x is present in linked list */
/*bool*/ std::tuple<bool, int> search(Node* head, int x)
{
    Node* current = head; // Initialize current
    int count = 0;
    while (current != NULL) {
        count++;
        if (current->data == x)

            return make_tuple(true, count);
        current = current->next;
    }
    return make_tuple(false, 0);
}

/* Counts no. of nodes in linked list */
int getCount(Node* head)
{
    int count = 0; // Initialize count
    Node* current = head; // Initialize current
    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}
/*Question: Why would one use recursion or a tail recursive function*/

// This function prints contents of linked
// list starting from the given node
void printList(Node* node)
{
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
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
    printList(head);

    //Function Calls
    //
    //
    /*Removes first node
     *
    removeFirstNode(head);
     */

    /* Removes last node
     *
    removeLastNode(head);
    */

    /* Removes node in certain position
     *
    deleteNode(head, 2);
    */

    /* Search for data and return position. (Does not distinguish multiple positions*/

    //search(head, x) ? cout << "Yes" : cout << "No";
    int x = 5;

    bool found;
    int position;
    std::tie(found, position) = search(head, x);
    cout << boolalpha << "\n If found and position: " << found << ":" << position << "\n" << endl;


    /* Count # of nodes */
    cout << "count of nodes is \n" << getCount(head) << "\n" << endl;
    printList(head);
    return 0;
}
```
