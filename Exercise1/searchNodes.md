```cpp
/* Checks whether the value x is present in linked list */
/*bool*/ std::tuple<bool, int> search(Node* head, int x) //Using a tuple in order to return two values in a sense
{
    Node* current = head; // Initialize current
    int count = 0;
    while (current != NULL) {
        count++;
        if (current->data == x)

            return make_tuple(true, count); // used make_tuple to not only grab if true but to also grab the position while we are here
        current = current->next;
    }
    return make_tuple(false, 0);
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
   
    /* Search for data and return position. (Does not distinguish multiple positions*/

    //search(head, x) ? cout << "Yes" : cout << "No";
    int x = 5;

    bool found;
    int position;
    std::tie(found, position) = search(head, x);
    cout << boolalpha << "\n If found and position: " << found << ":" << position << "\n" << endl; // boolalpha allows for the bool value in the tuple to print as true or false

    return 0;
}
```
