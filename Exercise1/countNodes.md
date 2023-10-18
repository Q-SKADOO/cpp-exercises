```cpp
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
