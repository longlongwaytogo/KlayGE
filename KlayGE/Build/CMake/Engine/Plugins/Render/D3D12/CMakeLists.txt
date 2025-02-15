if (NOT KLAYGE_PLATFORM_WINDOWS)
	return()
endif()

SET(LIB_NAME KlayGE_RenderEngine_D3D12)

SET(D3D12_RE_SOURCE_FILES
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Adapter.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12AdapterList.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Fence.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12FrameBuffer.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12GpuDescriptorAllocator.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12GpuMemoryAllocator.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12GraphicsBuffer.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12InterfaceLoader.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Query.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderEngine.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderFactory.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderLayout.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderStateObject.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderView.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12RenderWindow.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Resource.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12ShaderObject.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Texture.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Texture1D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Texture2D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Texture3D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12TextureCube.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12Util.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/D3D12/D3D12VideoMode.cpp
)

SET(D3D12_RE_HEADER_FILES
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Adapter.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12AdapterList.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Fence.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12FrameBuffer.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12GpuDescriptorAllocator.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12GpuMemoryAllocator.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12GraphicsBuffer.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12InterfaceLoader.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Query.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderEngine.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderFactory.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderLayout.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderStateObject.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderView.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12RenderWindow.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Resource.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12ShaderObject.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Texture.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12Util.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/D3D12/D3D12VideoMode.hpp
)

SOURCE_GROUP("Source Files" FILES ${D3D12_RE_SOURCE_FILES})
SOURCE_GROUP("Header Files" FILES ${D3D12_RE_HEADER_FILES})

ADD_LIBRARY(${LIB_NAME} SHARED
	${D3D12_RE_SOURCE_FILES} ${D3D12_RE_HEADER_FILES}
)

if(KLAYGE_COMPILER_GCC)
	# GCC warnings emitted by preprocessor can't be suppressed with pragma GCC diagnostic ignored
	target_compile_options(${LIB_NAME}
		PRIVATE
			-Wno-unknown-pragmas
	)
endif()

target_include_directories(${LIB_NAME}
	PRIVATE
		${KLAYGE_PROJECT_DIR}/Plugins/Include
)

SET_TARGET_PROPERTIES(${LIB_NAME} PROPERTIES
	PROJECT_LABEL ${LIB_NAME}
	OUTPUT_NAME ${LIB_NAME}${KLAYGE_OUTPUT_SUFFIX}
	FOLDER "KlayGE/Engine/Plugins/Render"
)
if(KLAYGE_PREFERRED_LIB_TYPE STREQUAL "SHARED")
	set_target_properties(${LIB_NAME} PROPERTIES
		CXX_VISIBILITY_PRESET hidden
		VISIBILITY_INLINES_HIDDEN ON
	)
endif()

KLAYGE_ADD_PRECOMPILED_HEADER(${LIB_NAME} "${KLAYGE_PROJECT_DIR}/Core/Include/KlayGE/KlayGE.hpp")

target_link_libraries(${LIB_NAME}
	PRIVATE
		${KLAYGE_CORELIB_NAME}
		DirectX-Headers
		dxsdk
)
IF(KLAYGE_PLATFORM_WINDOWS_STORE)
	target_link_libraries(${LIB_NAME}
		PRIVATE
			d3d12 dxgi dxguid
	)
ENDIF()

ADD_DEPENDENCIES(AllInEngine ${LIB_NAME})
