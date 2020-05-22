****I have used the training data given in this problem only to found out that regular expressions actually work 
best for these type of question where we are only supposed to extract the text from the image and search for a substring 
which contains the required attribute which in this case is the "Total Amount".****

Cell 1:
Importing all the essential libraries that I am using in this soln.

Cell 2:
Reading the test data and converting the test pdf documents to jpeg image.

Cell 3:
Image preprocessing for better pytesseract(used for extracting text form a given image) accuracy.
Adaptive Gausian Thresholding gives best results

Cell 4:
Setting DPI(Dots Per Inch) to 400,400

Cell 5:
Extracting text from the images using pyteseract function img_to_string

Cell 6:
**After executing cell 5 we still find some empty strings which means pytesseract struggles in extracting text
from these images. These images may have high background noise.**
In order to extract text from these images I first have to remove its background noise. For that I use my image_preprocessing
function defined in cell 3.

Cell 7:
Firstly I have stored every extracted text in a list 'l_test'.
Thus 'l_test' is a list of strings which contains \n(new line character) which I have used to split this string.
Eg:
l_test[0]='BOA\n(310) 278-205!\nO051a TABLE 308 #Party ae\nBAR L SyrCk: 13 13:22 12/20/17\nSeparate checks: 1-of-3\n1 CRAB CAKE 15.00\n1 SKIRT STK LUNCH 28 .00\nSub Total: 43 .00\nTax: 4.09\nSub Total: 47.09\n12/20 14:29 TOTAL: =a. 9\nSUGGESTED GRATUITY\n18% 8.48\n20h 9,42'
new_list[0]=['BOA',
  '(310) 278-205!',
  'O051a TABLE 308 #Party ae',
  'BAR L SyrCk: 13 13:22 12/20/17',
  'Separate checks: 1-of-3',
  '1 CRAB CAKE 15.00',
  '1 SKIRT STK LUNCH 28 .00',
  'Sub Total: 43 .00',
  'Tax: 4.09',
  'Sub Total: 47.09',
  '12/20 14:29 TOTAL: =a. 9',
  'SUGGESTED GRATUITY',
  '18% 8.48',
  '20h 9,42']
Now for every item in the new list there is a line(string) which contains 'Total Amount'.
In order to find this string I have used Regular expresion which has a function search that searches a substring in
a string.I have searched for subtotal,total and amount in text.
Eg:
new_list[0]=['BOA',
  '(310) 278-205!',
  'O051a TABLE 308 #Party ae',
  'BAR L SyrCk: 13 13:22 12/20/17',
  'Separate checks: 1-of-3',
  '1 CRAB CAKE 15.00',
  '1 SKIRT STK LUNCH 28 .00',
  'Sub Total: 43 .00',
  'Tax: 4.09',
  'Sub Total: 47.09',
  '12/20 14:29 TOTAL: =a. 9',
  'SUGGESTED GRATUITY',
  '18% 8.48',
  '20h 9,42']
total_string[0]=['Sub Total: 43 .00', 'Sub Total: 47.09', '12/20 14:29 TOTAL: =a. 9'] **only contains lines that contains subtotal,total and amount.
Then I have a new empty list-'final' in which I will append all the float values that I find in these strings. And finally
I take the maximum of all these float values(because there might be both subtotal and total in the string so we need the total value)
Eg:
total_string[0]=['Sub Total: 43 .00', 'Sub Total: 47.09', '12/20 14:29 TOTAL: =a. 9']
final[0]=47.09

Cell 8:
Writing predictions in the predictions file.


