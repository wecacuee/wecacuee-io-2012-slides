GOOGLE_IO_THEME_DIR=..

all: copy_src copy_theme copy_images

build/.dirstamp:
	mkdir build/
	touch build/.dirstamp

.PHONY: copy_theme copy_google_io_theme copy_src copy_images install

copy_theme: copy_google_io_theme

copy_google_io_theme: build/.dirstamp
	rsync -ruE ${GOOGLE_IO_THEME_DIR}/js ${GOOGLE_IO_THEME_DIR}/theme build/

copy_src: src/presentation-output.html src/slide_config.js build/.dirstamp
	mv src/presentation-output.html build/;\
	cp src/slide_config.js build/

copy_images: build/.dirstamp
	rsync -ruE ../images/ build/images/
	rsync -ruE src/images/ build/images/

src/presentation-output.html: src/presentation.md 
	cd src;\
	python render.py; cd -

install: all
	rsync -crvz build/ ubunix.buffalo.edu:~/public_html/cse740/
