# Operation in files
touch notes.txt ---- creates file with name notes <br>
echo "Line 1" > notes.txt -----add content to the line and over write if anything written<br>
echo "Line 2" >> notes.txt ----add content and append the content at the end it do not overwrite<br>
echo "Line 3" | tee -a notes.txt ---display the content as well as append at last. If -a not there it will overwrite<br>
cat notes.txt  ---displayes the overall output
head -n 2 notes.txt ---diaplays firat 2 line<br>
tail -n 2 notes.txt ---displays last 2 lines<br>
<img width="1025" height="487" alt="image" src="https://github.com/user-attachments/assets/1c18571c-51a7-4e3c-be24-b2456154a91c" />

# Negative scenarios of > and tee without -a will overwrite whole file
echo "Line 1" > notes.txt -----add content to the line and over write if anything written<br>
echo "Line 2" >> notes.txt ----add content and append the content at the end it do not overwrite<br>
echo "Line 3" | tee notes.txt ---display the content as well as append at last. If -a not there it will overwrite<br>
<img width="1032" height="227" alt="image" src="https://github.com/user-attachments/assets/25146a24-146f-4fa1-8b9a-535f993e8f3d" />
