Methodological Appendix
=======================

When using photogrammetry to create a 3D model it is essential that the visible
parts of the object remain in a constant relationship to each other. For
example, if one is creating a 3D model of a clay vase, it suffices to take many
photos from all sides and then construct a 3D model.

Using photogrammetry to make a 3D model of a book is complicated by the fact
that both sides of the book are of interest and that one needs to make 3D
models of each side of the book separately. These two 3D models can be merged
at a later point. In order to align the two 3D models it is vital that they
have common reference points. We created a common reference point by sticking a
small strip of paper into the book and making four crosses on both sides of the
paper (the crosses are aligned and at the exterior edge of the paper). This
strip of paper is inserted into the book such that the crosses are visible.
These crosses need to be clearly visible; we recommend a width of at least 3cm.

Step 1: Photography
-------------------

1. Attach camera to tripod
2. Place object on a piece of paper (on top of a mylar sheet) with clear scale markings (e.g. an indication of what 1cm is). If you have access to a turntable (a Lazy Susan works well), place everything on top of the turntable.
3. Adjust camera settings

    - Set f-stop to maximum (f. 8 to f. 12)
    - Disable flash
    - Make sure exposure is appropriate for light level.
    - Take a few test shots to ensure that all is working

4. Photograph object lying flat, rotating between shots.
    - Take 8-16 shots of object, rotating around the center of the object.
    - Raise or lower camera substantially, moving it closer or farther away as well, take another 8-16 shots, rotating around center of object.
    - Raise or lower camera substantially again, moving it closer or farther away as well, take another 8-16 shots, rotating around center of object.
    - Flip object over if you are concerned about the side that is not currently visible.
    - Repeat steps a, b, and c.

Step 2: VisualSFM
-----------------

Install a copy of the open-source software VisualSFM. On some platforms (e.g.
Linux) this step is comically difficult. There are numerous online tutorials
describing how to compile and use VisualSFM. Detailed instructions are beyond
the scope of this abstract.

For each side of the book you will need to perform the following steps.

1. Launch VisualSFM and use the menu item “Open+ Multi Images” to load all images associated with one side of the book.
2. Use the menu item “Compute Missing Matches”. This step is in some sense the essential one because it makes use of a technique which is at the core of photogrammetry, scale-invariant feature transform (SIFT). SIFT facilitates the identification of shared features in images even though the features may be visible at different scales.
3. Use the menu item “Sparse Reconstruction”
4. Use the menu item “Dense Reconstruction” and select a folder where the reconstruction will be saved.

Note: VisualSFM says that the maximum resolution it accepts for photos is
3200×2400. Most cameras take photos at a higher resolution than this. We found
that using lower-resolution images (e.g., width of 2600 pixels) does indeed
produce better results than using very-high resolution images (width of greater
than 4000 pixels). On Linux and OS X one can resize all JPG images in a
directory to a fixed width (preserving aspect ratio) with the following
one-line bash command and the ubiquitous open-source ImageMagick convert
program: ``for fn in *.JPG; do convert $fn -resize 2600 ${fn%.JPG}-lowres.jpg;
done``


Step 3: CloudCompare
--------------------

Use CloudCompare to align and merge the two point clouds (one for each book). CloudCompare
has an alignment tool that is designed for precisely this purpose. Once you have picked two sets of
matched points (at least 4 pairs) on the two clouds, CloudCompare will align
the two clouds. If the alignment is satisfactory, you may merge the clouds.

A final pass is required to remove extraneous points. This step is analogous
to cropping a photo. Use the *segment* tool for this step.
