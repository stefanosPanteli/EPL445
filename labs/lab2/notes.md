# δομικό παράθυρο για κάθε pixel

- `dilate / διαστολή`:  κάνω OR σε όλα τα pixel εντώς του παραθύρου
    - Αυξάνει το άσπρο (1), αν υπάρχει 1 άσπρο Pixel -> το κάνει
    - Μεγαλώνει τα αντικείμενα, ενώνει κοντινά (αν αντικείμενο είναι άσπρο)

- `erode / συστολή`: κάνω AND σε όλα τα pixel εντώς του παραθύρου
    - Μειώνει το άσπρο (1), πρέπει ΌΛΑ τα Pixel να είναι άσπρα για να το κάνει
    - Μικραίνουν τα αντικείμενα

<br>Υπάρχουν και συνδιασμοί:

- `opening: erosion -> dilate`
    - Καθαρίζει τα μικρά άσπρα spots
    - Αφαιρούνται μικρά αντικείμενα 

- `closing: dilate -> erosion`
    - Μειώνει τον θόρυβο. Καθαρίζει μαύρα spots.
    - Γεμίζει το εσωτερικό του αντικειμένου

<br>Συνήθως χρησημοποιούνται μαζί:
1. open -> close: ενώνει (όπως open)
2. close -> open: καθαρίζει (όπως close)


<br>***Στη θεωρία το 0 είναι το άσπρο, προγραμματιστικά το μαύρο.***




# Δομικά Στοιχεία:
```python
cv2.getStructuringElement(ARGS)
ARGS = (
    1. cv2.MORPH_RECT, (x,y) or
    2. cv2.MORPH_ELLIPSE, (x,y) or # Creates an ellipse inside an x by y rectangle
    3. cv2.MORPH_CROSS, (x,y)
)
```
# Πράξεις
```python
cv2.erode(image, kernel, iterations)
cv2.dilate(image, kernel, iterations)
cv2.morphologyEx(image, cv2.MORPH_OPEN, kernel)
cv2.morphologyEx(image, cv2.MORPH_CLOSE, kernel)
```


# Convert Image to Black and White
1. First turn the image grayscale
```python
image_gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
2. Then convert the image to black and white
```python
(threshold, image_bw) = cv2.threshhold(image_gray, Threshold, maxValue, cv2.THRESH_BINARY)
# Threshhold: int (threshold value)
# maxValue: int (maximum value of grayscale pixel (255))

# image_bw = (0 if pixel <= Threshhold else 1) for all pixels
```