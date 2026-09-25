# pole_of_inaccessibility
A pole of inaccessability is the point furthest from a given means of access. For land travel, it's Point Nemo in the South Pacific. This code is for finding poles of inaccessibility.

More specifically, the get_data notebook gets the bounding box of the White Mountain National Forest (WMNF), and then gets all the roads in the bbox, all the roads + trails in the bbox, and the perimeter of the WMNF. 

The wmnf_pole notebook gets the Voronoi tesselation of the road points (or road + trail points). A property of Voronoi tesselations is that one of the verticies (where cell edges meet) is the point at the center of the largest empty circle, which is to say the circle with none of the original points of the input to the tesselation (the centroids) in it. 

That means that if you use the points on roads as the seed points for the tesselation, one of the verticies is the point furthest from a road. This code does the tesselation, and then iterates the vertices, and for each vertex, records the minimum distance between the vertex and its centroid. The vertex with the largest minimum distance (LMD) is the center of the largest empty circle. 

There are a _lot_ of caveats to all this. First, the vertex with the LMD could be a vertex on the convex hull of the region rather than a Voronoi cell intersection vertex. I dealt with this by doing an unbounded Voronoi tesselation and then ignoring points in cells that had vertices at infinity, which throws out all the edge cells. Second, in a place like the WMNF, "hard to get to" and "far from roads" are not really related, if you consider metrics like elevation gain and difficulty of traversing terrain. This is ignored and the code acts like the WMNF is locally flat. Third, while the WMNF isn't locally flat, it isn't globally flat either. I did use geographiclib to try to get arc distances instead of straight line distances, but it's still an approximation. All maps are wrong, some maps are useful. 

If you just consider roads and ignore trails, or what OSM calls "tracks", the point is at https://maps.app.goo.gl/rNgPbEYXmv5R6oKM6 (44°08'09.6"N 71°30'33.8"W). It's in the Pemi Wilderness between Mt Bond and Hancock/Carriagain, near the east branch of the Pemigewasset River, about 2,500 feet west of the Thoreau Falls trail. 

So that's where you can find poles of inaccessability in the White Mountains. Enjoy, and don't end up in a Ty Gagne book!