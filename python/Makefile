all: olm-python2 olm-python3

include/olm/olm.h: ../include/olm/olm.h ../include/olm/inbound_group_session.h ../include/olm/outbound_group_session.h
	mkdir -p include/olm
	$(CPP) -I dummy -I ../include ../include/olm/olm.h -o include/olm/olm.h
# add memset to the header so that we can use it to clear buffers
	echo 'void *memset(void *s, int c, size_t n);' >> include/olm/olm.h

olm-python2: include/olm/olm.h
	DEVELOP=$(DEVELOP) python2 setup.py build

olm-python3: include/olm/olm.h
	DEVELOP=$(DEVELOP) python3 setup.py build

install: install-python2 install-python3

install-python2: olm-python2
	python2 setup.py install --skip-build -O1 --root=$(DESTDIR)

install-python3: olm-python3
	python3 setup.py install --skip-build -O1 --root=$(DESTDIR)

test: olm-python2 olm-python3
	rm -rf install-temp
	mkdir -p install-temp/2 install-temp/3
	PYTHONPATH=install-temp/2 python2 setup.py install --skip-build --install-lib install-temp/2 --install-script install-temp/bin
	PYTHONPATH=install-temp/3 python3 setup.py install --skip-build --install-lib install-temp/3 --install-script install-temp/bin
	PYTHONPATH=install-temp/3 python3 -m pytest
	PYTHONPATH=install-temp/2 python2 -m pytest
	PYTHONPATH=install-temp/3 python3 -m pytest --flake8 --benchmark-disable
	PYTHONPATH=install-temp/3 python3 -m pytest --isort --benchmark-disable
	PYTHONPATH=install-temp/3 python3 -m pytest --cov --cov-branch --benchmark-disable
	rm -rf install-temp

clean:
	rm -rf python_olm.egg-info/ dist/ __pycache__/
	rm -rf *.so _libolm.o
	rm -rf packages/
	rm -rf build/
	rm -rf install-temp/
	rm -rf include/

.PHONY: all olm-python2 olm-python3 install install-python2 install-python3 clean test
