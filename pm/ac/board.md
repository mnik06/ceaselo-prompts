### Block `board`: board with columns

- Every card sits in the column its current state names.
- Moving a card to another column changes the record's state, and the card is still there when the board is opened again.
- A move the rules forbid is refused visibly with the reason, and the card returns to its column.
- An empty column still shows its heading and a drop area, with no gap left between columns.
- A column with many cards scrolls on its own without moving the rest of the board.
