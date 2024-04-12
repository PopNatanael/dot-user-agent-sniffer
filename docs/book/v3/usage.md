# Usage

    <?php
    
    declare(strict_types=1);
    
    namespace Api\Example\Service;
    
    use Dot\UserAgentSniffer\Data\DeviceData;
    use Dot\UserAgentSniffer\Service\DeviceServiceInterface;
    
    /**
     * Class MyService
     * @package Api\Example\Service
     */
    class MyService
    {
        /** @var DeviceServiceInterface $deviceService */
        protected $deviceService;
    
        /**
         * MyService constructor.
         * @param DeviceServiceInterface $deviceService
         */
        public function __construct(DeviceServiceInterface $deviceService)
        {
            $this->deviceService = $deviceService;
        }
    
        /**
         * @param string $userAgent
         * @return DeviceData
         */
        public function myMethod(string $userAgent)
        {
            return $this->deviceService->getDetails($userAgent);
        }
    }

When called with an `$userAgent = 'Mozilla/5.0 (iPhone; CPU iPhone OS 13_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) CriOS/78.0.3904.84 Mobile/15E148 Safari/604.1'`, `myMethod($userAgent)` returns an object with the following structure:

    Dot\UserAgentSniffer\Data\DeviceData::__set_state(array(
        'type' => 'smartphone',
        'brand' => 'Apple',
        'model' => 'iPhone',
        'isBot' => false,
        'isMobile' => true,
        'os' =>
        Dot\UserAgentSniffer\Data\OsData::__set_state(array(
        'name' => 'iOS',
        'version' => '13.2',
        'platform' => '',
        )),
        'client' =>
        Dot\UserAgentSniffer\Data\ClientData::__set_state(array(
        'type' => 'browser',
        'name' => 'Chrome Mobile iOS',
        'engine' => 'WebKit',
        'version' => '78.0',
        )),
    ))

The above call can also be chained as `myMethod($userAgent)->getArrayCopy()`, to retrieve the details as an array:

    array (
        'type' => 'smartphone',
        'brand' => 'Apple',
        'model' => 'iPhone',
        'isMobile' => true,
        'isBot' => false,
        'os' =>
        array (
        'name' => 'iOS',
        'version' => '13.2',
        'platform' => '',
        ),
        'client' =>
        array (
        'type' => 'browser',
        'name' => 'Chrome Mobile iOS',
        'engine' => 'WebKit',
        'version' => '78.0',
        ),
    )
