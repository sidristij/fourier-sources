## DFT
- Сайт, наглядно объясняющий, что такое DFT, дискретное преобразование Фурье: https://www.jezzamon.com/fourier/index.html
 - Видеоролики, не менее наглядно объясняющие, что такое DFT, дискретное преобразование Фурье:
   - https://www.youtube.com/watch?v=r6sGWTCMz2k
   - https://www.youtube.com/watch?v=spUNpyF58BY
 - Анализатор сигнала с микрофона: https://www.compadre.org/osp/pwa/soundanalyzer/

## ThreadPool
- Станислав Сидристый, глава о ThreadPool: https://github.com/sidristij/dotnetbook/blob/master/book/ru/Execution/01-Threads/01-03-Threads-Thread-ThreadPool.md
- Станислав Сидристый, ThreadPool для сервиса, адаптирующегося под внешнюю нагрузку: https://www.youtube.com/watch?v=LbiuLwNJd1I
- Matt Warren, The CLR Thread Pool 'Thread Injection' Algorithm: https://mattwarren.org/2017/04/13/The-CLR-Thread-Pool-Thread-Injection-Algorithm/

## Java ThreadPools
 - Юрий Ткач, Сервис запуска потоков - Concurrency #3 - Advanced Java: https://www.youtube.com/watch?v=jFKrnW5ElMg
 - Алексей Шипилёв, Fork Join pool, особенности реализации: https://www.youtube.com/watch?v=_2ciDWeeXJQ

## Как менять свойства .NET ThreadPool

В startup проекте поменять

```
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
        <IsPackable>false</IsPackable>
        <TargetFramework>net5.0</TargetFramework>
    </PropertyGroup>

<!-- ... -->

    <ItemGroup>
        
        <!-- Common settings -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.MinThreads" Value="0" /> <!-- if 0, -> ProcessorCount -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.MaxThreads" Value="0" /> <!-- if 0, -> short.MaxValue -->
        
        <!-- Regulatins -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.CooperativeBlocking" Value="true" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.IgnoreMemoryUsage" Value="false" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.ThreadsToAddWithoutDelay_ProcCountFactor" Value="1" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.ThreadsPerDelayStep_ProcCountFactor" Value="1" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.DelayStepMs" Value="25" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.Blocking.MaxDelayMs" Value="250" />
        
        <!-- GateThread -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.DisableStarvationDetection" Value="false" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.DebugBreakOnWorkerStarvation" Value="false" />
        
        <!-- HillClimbing -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.Disable" Value="false" />

        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.WavePeriod" Value="4" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.MaxWaveMagnitude" Value="20" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.WaveMagnitudeMultiplier" Value="100" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.WaveHistorySize" Value="8" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.Bias" Value="15" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.TargetSignalToNoiseRatio" Value="300" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.MaxChangePerSecond" Value="4" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.MaxChangePerSample" Value="20" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.SampleIntervalLow" Value="10" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.SampleIntervalHigh" Value="200" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.ErrorSmoothingFactor" Value="1" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.GainExponent" Value="200" />
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.HillClimbing.MaxSampleErrorPercent" Value="15" />

        <!-- WorkerThread -->
        <RuntimeHostConfigurationOption Include="System.Threading.ThreadPool.UnfairSemaphoreSpinLimit" Value="70" />
        
    </ItemGroup>
    
</Project>

```
