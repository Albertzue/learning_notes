2025/9/21 page 57
2025/09/23 page 102
2025/09/26 page 126



1. Since this is a chargeable operation, another approach that can be used is to rename the new files with a version number and change the application to point to the new version. This will force the edge cache to be updated and the older version to expire and eventually be removed from the edge cache without incurring any charges. 
2. The best practice is to limit the use of invalidation requests and instead use an object versioning approach or shorten the header’s expiration time.
3. The Origin Shield service reduces the read load on the origin by adding an additional cache layer between the regional and edge locations and the origin
