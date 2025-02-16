# Tworzymy bibliotekę komponentów
add_library(nav_components
    core/Vector3D.cpp
    core/Quaternion.cpp
    core/Matrix.cpp
    filters/KalmanFilter.cpp
    filters/MadgwickFilter.cpp
    io/CSVHandler.cpp
    navigation/NavigationSystem.cpp
    navigation/DeadReckoning.cpp
    sensors/SensorData.cpp
    sensors/GPSData.cpp
)

target_include_directories(nav_components
    PUBLIC 
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/internal
)

# Linkujemy zależności
target_link_libraries(nav_components
    PUBLIC
        Eigen3::Eigen
)

# Definiujemy aplikację główną
add_executable(navigation_app
    app/main.cpp
)

# Linkujemy aplikację z biblioteką komponentów
target_link_libraries(navigation_app
    PRIVATE
        nav_components
)