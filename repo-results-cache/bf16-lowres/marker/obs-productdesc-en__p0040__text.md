**Table 6-2** lists the common operations supported by each system-defined policy or role of OBS. Select the policies or roles as required.

**Table 6-2** Permissions and the allowed operations on OBS resources

| Operatio<br>n                                      | Tenant<br>Administ<br>rator | Tenant<br>Guest | OBS<br>Administ<br>rator | OBS<br>Buckets<br>Viewer | OBS<br>ReadOnl<br>yAccess | OBS<br>Operate<br>Access |
|----------------------------------------------------|-----------------------------|-----------------|--------------------------|--------------------------|---------------------------|--------------------------|
| Listing<br>buckets                                 | Yes                         | Yes             | Yes                      | Yes                      | Yes                       | Yes                      |
| Creating<br>buckets                                | Yes                         | No              | Yes                      | No                       | No                        | No                       |
| Deleting<br>buckets                                | Yes                         | No              | Yes                      | No                       | No                        | No                       |
| Obtainin<br>g basic<br>bucket<br>informati<br>on   | Yes                         | Yes             | Yes                      | Yes                      | Yes                       | Yes                      |
| Controlli<br>ng<br>bucket<br>access                | Yes                         | No              | Yes                      | No                       | No                        | No                       |
| Managin<br>g bucket<br>policies                    | Yes                         | No              | Yes                      | No                       | No                        | No                       |
| Modifyin<br>g bucket<br>storage<br>classes         | Yes                         | No              | Yes                      | No                       | No                        | No                       |
| Listing<br>objects                                 | Yes                         | Yes             | Yes                      | No                       | Yes                       | Yes                      |
| Listing<br>objects<br>with<br>multiple<br>versions | Yes                         | Yes             | Yes                      | No                       | No                        | No                       |
| Uploadin<br>g files                                | Yes                         | No              | Yes                      | No                       | No                        | Yes                      |
| Creating<br>folders                                | Yes                         | No              | Yes                      | No                       | No                        | Yes                      |
| Deleting<br>files                                  | Yes                         | No              | Yes                      | No                       | No                        | Yes                      |