systemd_machined_sources = files('''
        machined.c
        machined.h
'''.split())

libmachine_core_sources = files('''
        machine.c
        machine.h
        machined-dbus.c
        machine-dbus.c
        machine-dbus.h
        image-dbus.c
        image-dbus.h
        operation.c
        operation.h
'''.split())

libmachine_core = static_library(
        'machine-core',
        libmachine_core_sources,
        include_directories : includes,
        dependencies : [threads])

if conf.get('ENABLE_MACHINED') == 1
        install_data('org.freedesktop.machine1.conf',
                     install_dir : dbuspolicydir)
        install_data('org.freedesktop.machine1.service',
                     install_dir : dbussystemservicedir)

        i18n.merge_file(
                'org.freedesktop.machine1.policy',
                input : 'org.freedesktop.machine1.policy.in',
                output : 'org.freedesktop.machine1.policy',
                po_dir : po_dir,
                data_dirs : po_dir,
                install : install_polkit,
                install_dir : polkitpolicydir)
endif

tests += [
        [['src/machine/test-machine-tables.c'],
         [libmachine_core,
          libshared],
         [threads],
         'ENABLE_MACHINED'],
]
