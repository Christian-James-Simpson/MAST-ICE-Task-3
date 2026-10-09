1. Line 13: Invalid Picker Import
Error: import { Picker } from '@expo/ui/community/picker';

Fix: Expo and React Native community recently moved or structure pickers differently, or if you are using @react-native-picker/picker, make sure the import matches your project dependencies. Standard Expo projects use @react-native-picker/picker.



2. Lines 63–66: Flawed Title Length Validation Logic
Error: title.trim().length < MIN_TEXT_LENGTH && title.trim().length > MAX_TITLE_LENGTH

Fix: Using && (AND) means this condition will never be true simultaneously (a string cannot be both shorter than 2 and greater than 50 at the same time). It needs to be an || (OR) operator



3. Lines 154 & 156: Type Mismatch in Temporary Album Object
Error: year: Number(year) and rating: Number(rating)

Fix: Your Album type definition (lines 15–21) defines year and rating as string, but you are assigning numbers to them. You should either update your Album interface to type them as number, or store them as strings (e.g., year: year.trim()).



4. Line 159: State Mutation Bug (Replacing Instead of Appending)
Error: setAlbums([temporaryAlbum]);

Fix: This replaces the entire array with just the single new album, violating the requirement that adding new albums should keep previous ones. You need to spread the current albums into the new array



5. Lines 169–171: Incorrect Deletion Logic in handleDelete
Error: currentAlbums.filter((album) => album.id === id)

Fix: The .filter() method keeps items that evaluate to true. This condition keeps only the item matching the deleted ID and removes everything else. To delete it, you must filter out the matching ID



6. Line 224: Incorrect Selected Value Binding on Picker
Error: selectedValue={title}

Fix: The Picker needs to reflect the genre state, not the title state



7. Line 230: Incorrect Value Prop on Picker Items
Error: <Picker.Item key="{item}" label="{item}" value="{genre}"/>

Fix: Every picker item is incorrectly setting its value to the global genre variable instead of the iteration variable item




8. Line 253: Faulty Key Extractor for FlatList
Error: keyExtractor={(item) => item.title}

Fix: If a user adds two albums with the same title, React Native will crash due to duplicate keys. You should use the unique id instead
