# Document export, maintaining the node structure

## Document export
* To export the document repository to a local path, maintaining the PaperTrail node structure as directories, add a Scheduled Rule from the Administration > Services section:
* Set the Schedule to 0 (Use the `Run Now` command to run the rule as required)
* Set the Query to the node you wish to export, including the checkbox `Search Nodes Below`
* Set `autoExport` as the Rule and `Folder` as the Mechanism
* In the Filename field, use `${node}/${filename}`
* Under Include, select `Source`

## Verify the exported document count
* Navigate to Administration > Services > Jobs
* Check the `Scheduled Rule: Export` job and note the number of documents processed under the Status field. Note: Documents of Type `Item (no file)` will naturally not export and will be counted under the failed status
* You can also check the results in the log file
