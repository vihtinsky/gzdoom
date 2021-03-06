cmake_minimum_required( VERSION 2.4 )
include( CheckCXXCompilerFlag )

make_release_only()

# I don't plan on debugging this, so make it a release build.
if( NOT CMAKE_BUILD_TYPE MATCHES "Release" )
	set( CMAKE_BUILD_TYPE "RelWithDebInfo" )
endif( NOT CMAKE_BUILD_TYPE MATCHES "Release" )

if( "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang" )
	set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra" )
	if( NOT PROFILE )
		set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fomit-frame-pointer" )
	endif( NOT PROFILE )
	check_cxx_compiler_flag( -Wno-array-bounds HAVE_NO_ARRAY_BOUNDS )
	if( HAVE_NO_ARRAY_BOUNDS )
		set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-array-bounds" )
	endif( HAVE_NO_ARRAY_BOUNDS )
endif( "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang" )

add_library( gme
    gme/Blip_Buffer.cpp
    gme/Classic_Emu.cpp
    gme/Data_Reader.cpp
    gme/Dual_Resampler.cpp
    gme/Effects_Buffer.cpp
    gme/Fir_Resampler.cpp
    gme/gme.cpp
    gme/Gme_File.cpp
    gme/M3u_Playlist.cpp
    gme/Multi_Buffer.cpp
    gme/Music_Emu.cpp
    
    gme/Ay_Apu.cpp
    gme/Ay_Cpu.cpp
    gme/Ay_Emu.cpp
    gme/Gb_Apu.cpp
    gme/Gb_Cpu.cpp
    gme/Gb_Oscs.cpp
    gme/Gbs_Emu.cpp
    gme/Gym_Emu.cpp
    gme/Hes_Apu.cpp
    gme/Hes_Cpu.cpp
    gme/Hes_Emu.cpp
    gme/Kss_Cpu.cpp
    gme/Kss_Emu.cpp
    gme/Kss_Scc_Apu.cpp
    gme/Nes_Apu.cpp
    gme/Nes_Cpu.cpp
    gme/Nes_Fme7_Apu.cpp
    gme/Nes_Namco_Apu.cpp
    gme/Nes_Oscs.cpp
    gme/Nes_Vrc6_Apu.cpp
    gme/Nsf_Emu.cpp
    gme/Nsfe_Emu.cpp
    gme/Sap_Apu.cpp
    gme/Sap_Cpu.cpp
    gme/Sap_Emu.cpp
    gme/Sms_Apu.cpp
    gme/Snes_Spc.cpp
    gme/Spc_Cpu.cpp
    gme/Spc_Dsp.cpp
    gme/Spc_Emu.cpp
    gme/Vgm_Emu.cpp
    gme/Vgm_Emu_Impl.cpp
    gme/Ym2413_Emu.cpp
    gme/Ym2612_Emu.cpp )
target_link_libraries( gme )
