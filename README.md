# Transitar Drive Inventory Data

Durable catalog of Google Drive folder inventories for Associacao Transitar.

- `drives.json`: ID-to-name map of the association's shared drives. The Drive connector cannot list or name shared drives, so this file is the single place drive names live. Maintained by hand.
- `folders/<name>_<id>.json`: one file per inventoried Drive folder, named by sanitized folder name + Drive ID. Flat; the tree is encoded inside the files (parent_id, subfolders, drive_id, folder_path). Latest inventory run replaces the content; git history is the archive.

Written by the `drive-folder-inventory` workflow (file entries) and the `drive-tree-describe` workflow (folder_description fields), both running on the drive-inventory-worker deployment. Exploration: read a directory listing for the catalog, open only the branch files of interest, or rebuild the full tree with a short script from parent_id links.

A folder's description is stale when any descendant's run.executed_at is newer than its folder_description_generated_at. Re-run drive-tree-describe to refresh.
