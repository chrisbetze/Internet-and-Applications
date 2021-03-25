# Internet-and-Applications
Web Project (Appathon) που υλοποιείται στο πλαίσιο του μαθήματος “Διαδίκτυο και Εφαρμογές” της Σχολής Ηλεκτρολόγων Μηχανικών και Μηχανικών Υπολογιστών του Εθνικού Μετσόβιου Πολυτεχνείου

## Περιγραφή της Εργασίας
To Project παρέχει στατιστικά δεδομένα σχετικά με τις τηλεπικοινωνίες και τον καιρό που επικρατούσε στην πόλη της Θεσσαλονίκης τους μήνες Αύγουστο και Νοέμβριο του 2019. 
Συγκεκριμένα, ανάλογα με την ημέρα που επιλέγεται από τον χρήστη, παρουσιάζονται με γραφική απεικόνιση οι δημοφιλέστερες ώρες, για κάθε τύπο δεδομένων: Τηλεφωνήματα, SMS, Data (χρήση της MySQL βάσης που δίνεται), καθώς και ο καιρός που επικρατούσε τις συγκεκριμένες ώρες (χρήση Web Service 12).
Επιπλεόν, υπάρχει η δυνατότητα απεικόνισης της τοποθεσίας των δημοφιλέστερων αποτελεσμάτων στο χάρτη. 
Τέλος, απεικονίζονται και τα live στατιστικά για κάθε τύπο δεδομένων, που λαμβάνουμε κάθε ένα λεπτό απο το Data Stream (MQTT broker).

## Τεχνολογίες που χρησιμοποιήθηκαν
Η υλοποίηση του Project πραγματοποιήθηκε με το **Node-Red** *(Node-Red-Dashboard)*. Επιπλέον, χρησιμοποιήθηκαν κάποια frameworks της JavaScript, όπως **Angular** *(Angular Material)* και κάποιες έξτρα βιβλιοθήκες για γραφικά όπως η **Chart.js**. Αναλυτικότερες πληροφορίες για τις βιβλιοθήκες και για τα nodes που χρησιμοποιήθηκαν θα περιγραφούν παρακάτω.

## Οδηγίες Εγκατάστασης-Εκτέλεσης του κώδικα
* Για να εγκατασταθεί το Node-Red τοπικά (locally) θα χρειαστεί το κατάλληλο version του Node.js. [δες εδώ](https://nodered.org/docs/faq/node-versions)
* Η εγκατάσταση μετά μπορεί να γίνει είτε με το *npm* command, είτε με άλλους τρόπους. [δες εδώ](https://nodered.org/docs/getting-started/local#installing-with-npm)
* Αφού εγκατασταθεί το Node-Red, μπορείτε να το τρέξετε από ένα τερματικό με την εντολή *node-red*.
* Με ανοιχτό το τερματικό υπάρχει πρόσβαση στον Node-Red Editor (http://localhost:1880), καθώς και στο project του Dashboard (http://localhost:1880/ui).
* Προκειμένου να μπορέσετε να δείτε ολοκληρωμένα την Εργασία, απαιτείται η εγκατάσταση ορισμένων ειδικών τύπων **Nodes**, η οποία μπορεί να γίνει, είτε μέσω της παλλέτας στον Node-Red Editor, είτε απευθείας από το τερματικό μέσω των εντολών που υπάρχουν στα αντίστοιχα links:
  * node-red-dashboard [link](https://flows.nodered.org/node/node-red-dashboard)
  * node-red-contrib-web-worldmap [link](https://flows.nodered.org/node/node-red-contrib-web-worldmap)
  * node-red-node-mysql [link](https://flows.nodered.org/node/node-red-node-mysql)
  * node-red-contrib-moment [link](https://flows.nodered.org/node/node-red-contrib-moment)
* Στην συνέχεια, για να δείτε και να επεξεργαστείτε την Εργασία θα πρέπει να κάνετε import το αρχείο με τα flows *(flows.json)*, που υπάρχει ανεβασμένο στο github.
* Τέλος, μπορείτε να περιηγηθείτε στην Εργασία, δηλαδή στο Dashboard, μέσω του συνδέσμου http://localhost:1880/ui.

**Προσοχή:** Στο αρχείο flows.json που δημιουργείτε όταν κάνουμε export τα flows, δεν μεταφέρονται τα security credentials, δηλαδή, δεν υπάρχουν τα στοιχεία ασφαλείας (**username** και **password**) για την βάση δεδομένων και τον mqtt broker. Επομένως, με το που γίνει το import, θα πρέπει να γράψετε τα στοιχεία ασφαλείας στα **mysql** nodes και στο **mqtt in** node.

## Περιγραφή της Υλοποίησης
Χωρίσαμε την εργασία σε 5 flows, όσες και οι καρτέλες (tabs) στο dashboard:
1. To **Home**: που είναι η αρχική σελίδα και παρέχει τις γενικές πληροφορίες για την εφαρμογή καθώς και τα live στατιστικά. Αποτελείται από διάφορα templates, buttons, ui controls, functions, chart nodes και έναν mqtt node in για την επικοινωνία με τον mqtt broken.
1. Το **Calls Statistics**: που παρέχει τις πληροφορίες για τα στατιστικά κλήσεων και τον καιρό. Αποτελείται από διάφορα templates, buttons, ui controls, functions, moment nodes, switch node, notification node, sql node και http request node.
1. Το **SMS Statistics**: που παρέχει τις πληροφορίες για τα στατιστικά SMS και τον καιρό. Αποτελείται από διάφορα templates, buttons, ui controls, functions, moment nodes, switch node, notification node, sql node και http request node.
1. Το **Data Statistics**: που παρέχει τις πληροφορίες για τα στατιστικά Data (Gbytes) και τον καιρό. Αποτελείται από διάφορα templates, buttons, ui controls, functions, moment nodes, switch node, notification node, sql node και http request node.
1. Το **Map**: που εμφανίζει στο χάρτη την τοποθεσία του δημοφιλέστερου αποτελέσματος. Αποτελείται από διάφορα templates, buttons, ui controls, functions, moment nodes, switch node, notification node, sql node και world map nodes.

Λεπτομερέστερη περιγραφή της υλοποίσησης και των Nodes που χρησιμοποιήθηκαν θα γίνει στην παρουσίαση και ιδιαίτερα στο βίντεο.
